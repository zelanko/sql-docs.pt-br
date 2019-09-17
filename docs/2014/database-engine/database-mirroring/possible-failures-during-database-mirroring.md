---
title: Possíveis falhas durante o espelhamento de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- time-out period [SQL Server database mirroring]
- soft errors [SQL Server]
- database mirroring [SQL Server], troubleshooting
- timeout errors [SQL Server]
- troubleshooting [SQL Server], database mirroring
- hard errors
- failed database mirroring sessions [SQL Server]
ms.assetid: d7031f58-5f49-4e6d-9a62-9b420f2bb17e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a380b3c4f27df6ad9d60fc27f14a4f5072c676a0
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874505"
---
# <a name="possible-failures-during-database-mirroring"></a>Possíveis falhas durante espelhamento de banco de dados
  Problemas físicos, do sistema operacional ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem causar uma falha em uma sessão de espelhamento de banco de dados. O espelhamento de banco de dados não verifica regularmente os componentes dos quais o Sqlservr.exe depende para verificar se estão funcionando corretamente ou se houve falha. Porém, para alguns tipos de falhas, o componente afetado informa um erro ao Sqlservr.exe. Um erro informado por outro componente é chamado um *erro de hardware*. Para detectar outras falhas que de outra forma passariam despercebidas, o espelhamento de banco de dados implementa seu próprio mecanismo de tempo limite. Quando ocorre um tempo limite de espelhamento, o espelhamento de banco de dados assume que ocorreu uma falha e declara um *erro de software*. Porém, algumas falhas que acontecem no nível da instância do SQL Server não causam espelhamento para tempo limite e podem não ser detectadas.  
  
> [!IMPORTANT]  
>  Falhas em bancos de dados diferentes do banco de dados espelho não são detectáveis em uma sessão de espelhamento de banco de dados. Além disso, é improvável que uma falha de disco de dados seja detectável, a menos que o banco de dados seja reiniciado por causa de uma falha no disco de dados.  
  
 A velocidade da detecção de erro e, consequentemente, o tempo de reação da sessão de espelhamento a uma falha depende do tipo de falha: de hardware ou de software. Alguns erros de hardware, como falhas de rede, são informados imediatamente. Porém, em alguns casos, períodos de tempo limite específicos do componente podem atrasar o relatório de alguns erros de hardware. Para erros de software, a duração do período de tempo limite de espelhamento determina a velocidade de detecção de erros. Por padrão, esse período é 10 segundos. Esse é o valor mínimo recomendado.  
  
## <a name="failures-due-to-hard-errors"></a>Falhas devido a erros de hardware  
 As possíveis causas de erros de hardware incluem (mas não se limitam a) as seguintes condições:  
  
-   Uma conexão ou um cabo interrompido  
  
-   Uma placa de rede incorreta  
  
-   Uma alteração no roteador  
  
-   Alterações no firewall  
  
-   Reconfiguração de ponto de extremidade  
  
-   Perda da unidade onde o log de transações reside  
  
-   Falha de sistema operacional ou de processo  
  
 Por exemplo, quando a unidade de log do banco de dados principal deixar de responder e apresentar falha, o sistema operacional informa ao Sqlservr.exe que ocorreu um erro grave.  
  
 Alguns componentes, como componentes de rede e alguns subsistemas de E/S, têm seus próprios tempos limite para determinar falhas. Esses tempos limite são independentes do espelhamento de banco de dados, que não tem conhecimento sobre eles e não sabe absolutamente nada sobre seu comportamento. Nesses casos o atraso do tempo limite aumenta o tempo entre uma falha e o momento em que o espelhamento do banco de dados recebe o erro de hardware resultante.  
  
> [!NOTE]  
>  A única verificação de erros ativa executada para espelhamento de banco de dados ocorre nos casos de erros de software. Para obter mais informações, consulte "Falhas devido a erros de software", mais adiante neste tópico.  
  
 Para ajudar o usuário a interpretar as condições de erro que ocorrem na rede, pergunte a um engenheiro de rede quais são as mensagens de erro enviadas a uma porta quando os seguintes eventos ocorrem em uma conexão TCP:  
  
-   DNS não está funcionando.  
  
-   Cabos estão desconectados.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] O Windows tem um firewall que bloqueia uma porta específica.  
  
-   Falha no aplicativo que está monitorando uma porta.  
  
-   Um servidor baseado no Windows é renomeado.  
  
-   Um servidor baseado no Windows é reinicializado.  
  
> [!NOTE]  
>  O espelhamento não protege contra problemas específicos para clientes que acessam os servidores. Considere, por exemplo, um caso em que um adaptador de rede pública controla as conexões do cliente com a instância do servidor principal, enquanto uma placa de interface de rede privada controla todo o tráfego de espelhamento entre as instâncias do servidor. Nesse caso, uma falha do adaptador de rede pública impediria os clientes de acessarem o banco de dados, embora o banco de dados continuasse a ser espelhado.  
  
## <a name="failures-due-to-soft-errors"></a>Falhas devido a erros recuperáveis  
 Condições que poderiam ocasionar tempos-limite de espelhamento incluem (mas não se limitam a) o seguinte:  
  
-   Erros de rede, como tempos-limite de link de TCP, pacotes descartados ou corrompidos ou pacotes que estão em ordem incorreta.  
  
-   Um sistema operacional, servidor ou banco de dados que não está respondendo.  
  
-   Um servidor Windows que atingiu o tempo limite.  
  
-   Recursos computacionais insuficientes, tais como sobrecarga de uma CPU ou disco, filling up do log de transações ou o sistema está sendo executado sem memória ou threads. Nesses casos, é preciso aumentar o período de tempo limite, reduzir a carga de trabalho ou alterar o hardware para controlar a carga de trabalho.  
  
### <a name="the-mirroring-time-out-mechanism"></a>O mecanismo de tempo-limite de espelhamento  
 Como os erros recuperáveis não são diretamente detectáveis por uma instância do servidor, um erro recuperável poderia potencialmente fazer uma instância do servidor aguardar indefinidamente. Para evitar isso, o espelhamento de banco de dados implementa seu próprio mecanismo de tempo-limite com base em cada instância do servidor em uma sessão de espelhamento enviando um ping em cada conexão aberta em um intervalo fixo.  
  
 Para manter uma conexão aberta, uma instância do servidor deve receber um ping naquela conexão dentro do período de tempo-limite definido, mais o tempo necessário para enviar um ou mais pings. A recepção de um ping durante o período de tempo-limite indica que a conexão ainda está aberta e que as instâncias do servidor estão se comunicando por ela. Ao receber um ping, uma instância do servidor reajusta seu contador de tempo-limite naquela conexão.  
  
 Se nenhum ping for recebido em uma conexão durante o período de tempo-limite, uma instância do servidor considera que a conexão esgotou seu tempo limite. A instância do servidor encerra a conexão cujo tempo-limite está esgotado e controla o evento com tempo-limite esgotado de acordo com o estado e o modo de operação da sessão.  
  
 Até mesmo se o outro servidor estiver de fato procedendo corretamente, um tempo-limite será considerado uma falha. Se o valor do tempo-limite de uma sessão for muito pequeno para uma capacidade de resposta regular de um dos parceiros, podem ocorrer falsas falhas. Uma falsa falha ocorre quando uma instância do servidor contata com êxito outra instância cujo tempo de resposta é tão lento que seus pings não são recebidos antes da expiração do período de tempo-limite.  
  
 Em sessões de modo de grande desempenho, o período de tempo-limite é sempre 10 segundos. Esse tempo é geralmente suficiente para evitar falsas falhas. Em sessões de modo da segurança alta, o período de tempo-limite padrão é 10 segundos, mas é possível alterá-lo. Para evitar falsas falhas, recomendamos que o período de tempo-limite de espelhamento seja sempre de 10 segundos ou mais.  
  
 **Para alterar o valor de tempo-limite (somente modo de segurança alta)**  
  
-   Use a instrução [ALTER DATABASE \<database> SET PARTNER TIMEOUT \<integer>](/sql/t-sql/statements/alter-database-transact-sql).  
  
 **Exibir o valor atual de tempo-limite**  
  
-   Consulte **mirroring_connection_timeout** em [sys.database_mirroring](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql).  
  
## <a name="responding-to-an-error"></a>Respondendo a um erro  
 Independentemente do tipo de erro, uma instância do servidor que detecta um erro responde adequadamente com base na função da instância, no modo de operação da sessão e no estado de qualquer outra conexão na sessão. Para obter informações sobre o que ocorre na perda de um parceiro, consulte [Modos de operação de espelhamento de banco de dados](database-mirroring-operating-modes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Estimar a interrupção do serviço durante troca de função &#40;Espelhamento de Banco de Dados&#41;](estimate-the-interruption-of-service-during-role-switching-database-mirroring.md)   
 [Modos de operação de espelhamento de banco de dados](database-mirroring-operating-modes.md)   
 [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
