---
title: Procedimento armazenados (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- storing programs as stored procedures
- stored procedures [SQL Server], about stored procedures
ms.assetid: cc6daf62-9663-4c3e-950a-ab42e2830427
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: dd0517fa69865cd3a4d3180071be0551606a5090
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="stored-procedures-database-engine"></a>Procedimento armazenados (Mecanismo de Banco de Dados)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Um procedimento armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um grupo de uma ou mais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] ou uma referência a um método CLR (Common Language Runtime) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Os procedimentos lembram as construções em outras linguagens de programação porque podem:  
  
-   Aceitar parâmetros de entrada e retornar vários valores no formulário de parâmetros de saída para o programa de chamada.  
  
-   Conter instruções de programação que executam operações no banco de dados. Estas incluem a chamada de outros procedimentos.  
  
-   Retornar um valor de status a um programa de chamada para indicar êxito ou falha (e o motivo da falha).  
  
## <a name="benefits-of-using-stored-procedures"></a>Benefícios do uso de procedimentos armazenados  
 A lista a seguir descreve alguns benefícios do uso de procedimentos.  
  
 Tráfego de rede de servidor/cliente reduzido  
 Os comandos em um procedimento são executados como um único lote de código. Isso pode reduzir significativamente o tráfego da rede entre cliente e servidor porque a única chamada para executar o procedimento é enviada pela rede. Sem o encapsulamento de código fornecido por um procedimento, cada linha individual de código teria de cruzar a rede.  
  
 Segurança mais forte  
 Vários usuários e programas cliente podem executar operações em objetos de banco de dados subjacentes por meio de um procedimento, mesmo se os usuários e programas não tiverem permissões diretas nesses objetos subjacentes. O procedimento controla quais processos e atividades são executados e protege os objetos de banco de dados subjacentes. Isso elimina a necessidade de conceder permissões no nível de objeto individual e simplifica as camadas de segurança.  
  
 A cláusula [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) pode ser especificada na instrução CREATE PROCEDURE para permitir a representação de outro usuário, ou permitir que usuários ou aplicativos executem certas atividades de bancos de dados sem precisar de permissões diretas nos objetos e comandos subjacentes. Por exemplo, algumas ações como TRUNCATE TABLE, não têm permissões concessíveis. Para executar TRUNCATE TABLE, o usuário deve ter permissões ALTER na tabela especificada. A concessão de permissões ALTER a um usuário em uma tabela pode não ser ideal porque o usuário irá, efetivamente, ter permissões a mais do que a capacidade de truncar uma tabela. Incorporando a instrução TRUNCATE TABLE em um módulo e especificando que o módulo executa como um usuário que tem permissões para modificar a tabela, você pode estender as permissões para truncar a tabela para o usuário ao qual você concedeu permissões EXECUTE no módulo.  
  
 Ao chamar um procedimento na rede, somente a chamada para executar o procedimento ficará visível. Portanto, usuários mal-intencionados não podem consultar nomes de tabelas e objetos de banco de dados, inserir instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] próprias nem pesquisar para obter dados críticos.  
  
 Usar parâmetros de procedimento ajuda na proteção contra ataques de injeção SQL. Como a entrada de parâmetro é tratada como valor literal e não como código executável, fica mais difícil para um invasor inserir um comando nas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] dentro do procedimento e comprometer a segurança.  
  
 Os procedimentos podem ser criptografados, ajudando a ofuscar o código-fonte. Para obter mais informações, veja [Criptografia do SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md).  
  
 Reutilização de código  
 O código para qualquer operação de banco de dados redundante é o candidato perfeito para encapsulamento em procedimentos. Isso elimina regravações desnecessárias do mesmo código, reduz a inconsistência de códigos e permite que o código seja acessado e executado por qualquer usuário ou aplicativo que possui as permissões necessárias.  
  
 Manutenção facilitada  
 Quando aplicativos cliente chamam procedimentos e mantêm as operações de banco de dados na camada de dados, somente os procedimentos devem ser atualizados com qualquer alteração no banco de dados subjacente. A camada de aplicativos permanece separada e não precisa saber das alterações de layouts, relações ou processos de bancos de dados.  
  
 Melhor desempenho  
 Por padrão, um procedimento é compilado na primeira vez em que é executado e cria um plano de execução que é reutilizado em execuções subsequentes. Como o processador de consulta não precisa criar um novo plano, normalmente demora menos tempo para processar o procedimento.  
  
 Se houver alterações significantes nas tabelas ou dados referenciados pelo procedimento, o plano pré-compilado poderá, na verdade, fazer com que o procedimento execute mais lentamente. Neste caso, recompilar o procedimento e forçar um novo plano de execução podem melhorar desempenho.  
  
## <a name="types-of-stored-procedures"></a>Tipos de procedimentos armazenados  
 Definido pelo usuário  
 Um procedimento definido pelo usuário pode ser criado em um banco de dados definido pelo usuário ou em todos os bancos de dados do sistema, exceto no banco de dados **Resource** . O procedimento pode ser desenvolvido em [!INCLUDE[tsql](../../includes/tsql-md.md)] ou como referência para um método CLR da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
 Temporário  
 Procedimentos temporários são uma forma de procedimentos definidos pelo usuário. Os procedimentos armazenados são como um procedimento permanente, exceto que os procedimentos temporários são armazenados em **tempdb**. Há dois tipos de procedimentos temporários: local e global. Elas diferem uma da outra pelo nome, visibilidade e disponibilidade. Os procedimentos temporários locais têm um único sinal numérico (#) como primeiro caractere no nome; eles são visíveis somente na conexão atual do usuário e são excluídas quando a conexão é fechada. Os procedimentos temporários globais têm dois sinais numéricos (##) como os dois primeiros caracteres de seus nomes; ficam visíveis para qualquer usuário depois de criados e são excluído no final da última sessão do procedimento.  
  
 Sistema  
 Os procedimentos do sistema são fornecidos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eles são fisicamente armazenados no banco de dados **Resource** interno oculto, e logicamente aparecem no esquema **sys** de cada banco de dados definido pelo sistema e pelo usuário. Além disso, o banco de dados **msdb** também pode conter procedimentos armazenados do sistema no esquema **dbo** que são usados para agendar alertas e trabalhos. Como os procedimentos do sistema começam com o prefixo **sp_**, recomendamos que você não use esse perfil quando for nomear procedimentos definidos pelo usuário. Para obter uma lista completa de procedimentos do sistema, veja [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md).  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte aos procedimentos do sistema que fornecem uma interface no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a programas externos para várias atividades de manutenção. Esses procedimentos estendidos usam o prefixo xp_. Para obter uma lista completa de procedimentos estendidos, veja [Procedimentos armazenados estendidos gerais &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md).  
  
 Extensões definidas pelo usuário  
 Os procedimentos estendidos permitem criar rotinas externas em uma linguagem de programação como C. Esses procedimentos são DLLs que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode carregar e executar dinamicamente.  
  
> [!NOTE]  
>  Os procedimentos armazenados estendidos são removidos de uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não utilize esse recurso em desenvolvimentos novos e modifique, assim que possível, os aplicativos que atualmente o utilizam. Crie procedimentos CLR, então. O método fornece uma alternativa mais robusta e segura para gravar procedimentos estendidos.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|||  
|-|-|  
|**Descrição da tarefa**|**Tópico**|  
|Descreve como criar um procedimento armazenado.|[Criar um procedimento armazenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)|  
|Descreve como modificar um procedimento armazenado.|[Modificar um procedimento armazenado](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)|  
|Descreve como excluir um procedimento armazenado.|[Excluir um procedimento armazenado](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)|  
|Descreve como executar um procedimento armazenado.|[Executar um procedimento armazenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)|  
|Descreve como conceder permissões em um procedimento armazenado.|[Conceder permissões em um procedimento armazenado](../../relational-databases/stored-procedures/grant-permissions-on-a-stored-procedure.md)|  
|Descreve como retornar dados de um procedimento armazenado para um aplicativo.|[Retornar dados de um procedimento armazenado](../../relational-databases/stored-procedures/return-data-from-a-stored-procedure.md)|  
|Descreve como recompilar um procedimento armazenado.|[Recompilar um procedimento armazenado](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)|  
|Descreve como renomear um procedimento armazenado.|[Renomear um procedimento armazenado](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)|  
|Descreve como exibir definições de um procedimento armazenado.|[Exibir a definição de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)|  
|Descreve como exibir as dependências de um procedimento armazenado.|[Exibir as dependências de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)|  
|Descreve como os parâmetros são usados em um procedimento armazenado.|[Parâmetros](../../relational-databases/stored-procedures/parameters.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Procedimentos armazenados CLR](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)  
  
  
