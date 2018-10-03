---
title: Reduzir a carga de ajuste do servidor de produção | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- overhead [Database Engine Tuning Advisor]
- tuning overhead [SQL Server]
- reducing production server tuning load
- Database Engine Tuning Advisor [SQL Server], test servers
- test servers [Database Engine Tuning Advisor]
- production servers [SQL Server]
- offload tuning overhead [SQL Server]
ms.assetid: bb95ecaf-444a-4771-a625-e0a91c8f0709
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fe8a6be944df0de60117edc1f800c38a449125e8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48175126"
---
# <a name="reduce-the-production-server-tuning-load"></a>Reduzir a carga de ajuste do servidor de produção
  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] O Orientador de Otimização usa o otimizador de consulta para analisar uma carga de trabalho e fazer recomendações de ajuste. Executar essa análise no servidor de produção aumenta a carga do servidor e pode prejudicar o desempenho do servidor durante a sessão de ajuste. É possível diminuir o impacto na carga do servidor durante uma sessão de ajuste usando um servidor de teste além do servidor de produção.  
  
## <a name="how-database-engine-tuning-advisor-uses-a-test-server"></a>Como o Orientador de Otimização de Mecanismo de Banco de Dados usa um servidor de teste  
 O modo tradicional de uso de um servidor de teste é copiar todos os dados de seu servidor de produção no servidor de teste, ajustar o servidor de teste e depois implementar a recomendação no seu servidor de produção. Esse processo elimina o impacto de desempenho em seu servidor de produção, mas, mesmo assim, não é a melhor solução. Por exemplo, copiar grandes volumes de dados da produção no servidor de teste pode consumir tempo e recursos significativos. Além disso, o hardware do servidor de teste raramente é tão eficiente quanto o hardware implantado nos servidores de produção. O processo de ajuste depende do otimizador de consulta, e as recomendações geradas são, em parte, baseadas no hardware subjacente. Se o hardware dos servidores de teste e de produção não for idêntico, a qualidade da recomendação do Orientador de Otimização do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] será menor.  
  
 Para evitar problemas desse tipo, o Orientador de Otimização do Mecanismo do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] ajusta um banco de dados em um servidor de produção descarregando a maioria da carga de ajuste em um servidor de teste. Ele faz isso usando as informações de configuração de hardware do servidor de produção, sem, de fato, copiar os dados do servidor de produção no servidor de teste. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] não copia dados reais do servidor de produção para o servidor de teste. Ele apenas copia os metadados e as estatísticas necessárias.  
  
 As etapas seguintes esboçam o processo para ajustar um banco de dados de produção em um servidor de teste:  
  
1.  Verifique se o usuário que deseja usar o servidor de teste existe nos dois servidores.  
  
     Antes de começar, verifique se o usuário que deseja usar o servidor de teste para ajustar um banco de dados no servidor de produção existe em ambos os servidores. Isso requer que você crie o usuário e o logon dele no servidor de teste. Se você for um membro da função de servidor fixa **sysadmin** nos dois computadores, essa etapa será desnecessária.  
  
2.  Ajuste a carga de trabalho no servidor de teste.  
  
     Para ajustar a carga de trabalho em um servidor de teste,é necessário usar um arquivo de entrada XML com o utilitário de linha de comando **dta** . No arquivo de entrada XML, especifique o nome de seu servidor de teste com o subelemento **TestServer** além de especificar os valores para os outros subelementos no elemento pai **TuningOptions** .  
  
     Durante o processo de ajuste, o Orientador de Otimização do Mecanismo do Banco de Dados cria um banco de dados shell no servidor de teste. Para criar esse banco de dados shell e ajustá-lo, o Orientador de Otimização do Mecanismo do Banco de Dados faz chamadas ao servidor de produção para o seguinte:  
  
    1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] O Orientador de Otimização importa metadados do banco de dados de produção para o banco de dados shell do servidor de teste. Esses metadados incluem tabelas vazias, índices, exibições, procedimentos armazenados, disparadores, e assim por diante. Isso possibilita a execução de consultas de carga de trabalho no banco de dados shell do servidor de teste.  
  
    2.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] O Orientador de Otimização importa estatísticas do servidor de produção para que o otimizador de consulta possa otimizar as consultas com precisão no servidor de teste.  
  
    3.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] O Orientador de Otimização importa parâmetros de hardware que especificam o número de processadores e a memória disponível do servidor de produção para fornecer ao otimizador de consulta as informações necessárias para gerar um plano de consulta.  
  
3.  Depois que o Orientador de Otimização do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] termina de ajustar o banco de dados shell do servidor de teste, ele gera uma recomendação de ajuste.  
  
4.  Aplique a recomendação recebida para ajustar o servidor de teste ao servidor de produção.  
  
 A ilustração a seguir mostra o servidor de teste e o cenário do servidor de produção:  
  
 ![Uso do servidor de teste do Orientador de Otimização do Mecanismo de Banco de Dados](../../database-engine/media/testsvr.gif "Uso do servidor de teste do Orientador de Otimização do Mecanismo de Banco de Dados")  
  
> [!NOTE]  
>  O recurso de ajuste do servidor de teste não é suportado na interface gráfica de usuário do Orientador de Otimização do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] .  
  
## <a name="example"></a>Exemplo  
 Primeiro, verifique se o usuário que deseja executar o ajuste existe nos servidores de produção e no de teste.  
  
 Depois que as informações de usuário são copiadas no servidor de teste, você pode definir a sessão de ajuste do servidor de teste no arquivo de entrada XML do Orientador de Otimização do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] . O exemplo de arquivo de entrada XML a seguir ilustra como especificar um servidor de teste para ajustar um banco de dados com o Orientador de Otimização do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] .  
  
 Neste exemplo, o banco de dados `MyDatabaseName` está sendo ajustado no `MyServerName`. O script [!INCLUDE[tsql](../../includes/tsql-md.md)] , `MyWorkloadScript.sql`, é usado como a carga de trabalho. Essa carga de trabalho contém eventos que são executados no `MyDatabaseName`. A maioria das chamadas de otimizador de consulta a esse banco de dados, que acontecem como parte do processo de ajuste, é controlada pelo banco de dados shell que reside no `MyTestServerName`. O banco de dados shell é composto de metadados e estatísticas. Esse processo resulta na sobrecarga do ajuste sendo descarregada no servidor de teste. Quando o Orientador de Otimização do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] gera a recomendação de ajuste usando esse arquivo de entrada XML, ele deve considerar somente índices (`<FeatureSet>IDX</FeatureSet>`) , nenhum particionamento e não deve manter nenhuma estrutura de design físico existente em `MyDatabaseName`.  
  
```  
<?xml version="1.0" encoding="utf-16" ?>  
<DTAXML xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/sqlserver/2004/07/dta">  
  <DTAInput>  
    <Server>  
      <Name>MyServerName</Name>  
      <Database>  
        <Name>MyDatabaseName</Name>  
      </Database>  
    </Server>  
    <Workload>  
      <File>MyWorkloadScript.sql</File>  
    </Workload>  
    <TuningOptions>  
      <TestServer>MyTestServerName</TestServer>  
      <FeatureSet>IDX</FeatureSet>  
      <Partitioning>NONE</Partitioning>  
      <KeepExisting>NONE</KeepExisting>  
    </TuningOptions>  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Considerações para usar servidores de teste](considerations-for-using-test-servers.md)   
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](database-engine-tuning-advisor.md)  
  
  
