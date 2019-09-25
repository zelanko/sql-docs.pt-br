---
title: Recuperação de banco de dados acelerada | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: kfarlee
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- accelerated database recovery [SQL Server], recovery-only
- database recovery [SQL Server]
author: mashamsft
ms.author: mathoma
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5bfd7d5585e08a643575f0c657c936e6a56b3f0c
ms.sourcegitcommit: 183d622fff36a22b882309378892010be3bdcd52
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71130555"
---
# <a name="accelerated-database-recovery"></a>Recuperação de banco de dados acelerada

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

A ADR (recuperação acelerada de banco de dados) melhora a disponibilidade do banco de dados, especialmente na presença de transações de execução prolongada, remodelando o processo de recuperação do mecanismo de banco de dados SQL. A ADR é uma novidade no SQL Server 2019 e também está disponível para bancos de dados individuais e bancos de dados em pool no Banco de Dados SQL do Azure e bancos de dados no SQL Data Warehouse do Azure (atualmente em versão prévia pública). Os principais benefícios do ADR são:

- **Recuperação de banco de dados rápida e consistente**

  Com a ADR, as transações de execução prolongada não afetam o tempo de recuperação geral, permitindo uma recuperação de banco de dados rápida e consistente, independentemente do número de transações ativas no sistema ou do tamanho delas.

- **Reversão de transação instantânea**

  Com ADR, a reversão de transação é instantânea, independentemente do tempo em que a transação esteve ativa ou do número de atualizações que ela realizou.

- **Truncamento agressivo do log**

  Com a ADR, o log de transações é truncado agressivamente, mesmo na presença de transações de execução prolongada ativas, o que impede que ele cresça fora de controle.

## <a name="the-current-database-recovery-process"></a>O processo de recuperação de banco de dados atual

Sem a ADR, a recuperação de banco de dados no SQL Server segue o modelo de recuperação [ARIES](https://people.eecs.berkeley.edu/~brewer/cs262/Aries.pdf) e consiste em três fases, que são ilustradas no diagrama a seguir e explicadas em mais detalhes após o diagrama.

![processo de recuperação atual](./media/accelerated-database-recovery-concepts/current-recovery-process.png)

- **Fase de análise**

  O SQL Server realiza uma verificação antecipada do log de transações desde o início do último ponto de verificação bem-sucedido (ou o LSN de página suja mais antigo) até o fim, para determinar o estado de cada transação no momento da interrupção do SQL Server.

- **Fase refazer**

  O SQL Server executa a verificação antecipada do log de transações da transação não confirmada mais antiga até o final, para colocar o banco de dados no estado em que estava no momento da falha, refazendo todas as operações confirmadas.

- **Fase desfazer**

  Para cada transação que estava ativa no momento da falha, o SQL Server percorre o log em sentido reverso, desfazendo as operações realizadas por essa transação.

Com base nesse design, o tempo necessário para que o mecanismo de banco de dados se recupere de uma reinicialização inesperada é (aproximadamente) proporcional ao tamanho da transação ativa mais longa no sistema no momento da falha. A recuperação requer uma reversão de todas as transações incompletas. O período de tempo necessário é proporcional ao trabalho que a transação realizou e à hora em que ela esteve ativa. Portanto, o processo de recuperação de SQL Server pode levar muito tempo se existirem transações de execução prolongada (como operações de inserção em massa grandes ou operações de build de índice em uma tabela grande).

Além disso, cancelar ou reverter uma transação grande baseada nesse design também pode levar muito tempo, pois esse processo está usando a mesma fase desfazer recuperação descrita acima.

Além disso, o mecanismo de banco de dados não pode truncar o log de transações quando há transações de execução prolongada, porque os registros de log correspondentes dessas transações são necessários para os processos de recuperação e reversão. Como resultado, alguns logs de transações tornam-se muito grandes e consomem grandes quantidades de espaço na unidade.

## <a name="the-accelerated-database-recovery-process"></a>O processo de recuperação acelerada de banco de dados

A ADR aborda os problemas acima remodelando completamente o processo de recuperação do mecanismo de banco de dados para:

- Torná-lo de tempo constante/instantâneo, evitando a necessidade de verificar o log de/para o início da transação ativa mais antiga. Com a ADR, o log de transações só é processado desde o último ponto de verificação bem-sucedido ou do LSN (número de sequência de log) de página suja mais antigo. Como resultado, o tempo de recuperação não é afetado por transações de execução prolongada.
- Minimize o espaço de log de transações necessário, pois não há mais necessidade de processar o log para toda a transação. Como resultado, o log de transações pode ser truncado agressivamente, pois ocorrem pontos de verificação e backups.

Em um nível alto, a ADR alcança a recuperação rápida do banco de dados ao realizar o controle de versão de todas as modificações físicas do banco de dados e desfazer apenas operações lógicas, que são limitadas e podem ser desfeitas quase instantaneamente. Todas as transações que estavam ativas no momento de uma falha são marcadas como anuladas e, portanto, todas as versões geradas por essas transações podem ser ignoradas por consultas de usuário simultâneas.

O processo de recuperação ADR tem as mesmas três fases que o processo de recuperação atual. A forma como essas fases operam com ADR é ilustrada no diagrama a seguir.

![Processo de recuperação de ADR](./media/accelerated-database-recovery-concepts/adr-recovery-process.png)

- **Fase de análise**

  O processo permanece o mesmo que hoje, com a adição da recriação de sLog e a cópia de registros de log para operações sem controle de versão.
  
- Fase **refazer**

  Dividida em duas subfases
  - Subfase 1

      Refazer de sLog (transação não confirmada mais antiga até o último ponto de verificação). Refazer é uma operação rápida, pois ela só precisa processar alguns registros do sLog.

  - Subfase 2

     Refazer do log de transações começa do último ponto de verificação (e não da transação não confirmada mais antiga)
     
- **Fase desfazer**

   A fase desfazer com a ADR é concluída quase instantaneamente usando o sLog para desfazer operações sem controle de versão e o PVS (repositório de versão persistente) com a reversão lógica para executar desfazer baseado em versão de nível de linha.

## <a name="adr-recovery-components"></a>Componentes de recuperação ADR

Os quatro principais componentes de ADR são:

- **PVS (repositório de versão persistente)**

  O repositório de versão persistente é um mecanismo de banco de dados para persistir as versões de linha geradas no banco de dados propriamente dito, em vez do repositório de versão `tempdb` tradicional. O PVS habilita o isolamento de recursos e melhora a disponibilidade de secundários legíveis.

- **Reversão lógica**

  A reversão lógica é o processo assíncrono responsável por executar a operação desfazer baseada em versão de linha, fornecendo reversão de transação instantânea e desfazer para todas as operações com controle de versão.

  - Mantém o controle de todas as transações anuladas
  - Executa a reversão usando PVS para todas as transações de usuário
  - Libera todos os bloqueios imediatamente após a anulação da transação

- **sLog**

  O sLog é um fluxo de log na memória secundário que armazena registros de log para operações sem controle de versão (tais como invalidação de cache de metadados, aquisições de bloqueio e assim por diante). O sLog é:

  - de baixo volume e na memória;
  - persistido no disco ao ser serializado durante o processo de ponto de verificação;
  - truncado periodicamente conforme as transações são confirmadas;
  - acelera as operações refazer e desfazer ao processar apenas as operações sem controle de versão;  
  - habilita o truncamento agressivo de log de transações ao preservar apenas os registros de log necessários.

- **Limpador**

  O limpador é o processo assíncrono que é ativado periodicamente e limpa as versões de página que não são necessárias.

## <a name="who-should-consider-accelerated-database-recovery"></a>Quem deve considerar usar a recuperação de banco de dados acelerada

Os seguintes tipos de clientes devem considerar habilitar a ADR:

- Clientes que têm cargas de trabalho com transações de execução prolongada.
- Clientes que viram casos em que as transações ativas estão causando aumento significativo do log de transações.  
- Clientes que tiveram longos períodos de indisponibilidade de banco de dados devido a recuperação de execução prolongada do SQL Server (assim como reinicialização inesperada do SQL Server ou reversão de transação manual).


## <a name="see-also"></a>Consulte Também  

  
