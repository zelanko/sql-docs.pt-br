---
title: Executando o supervisor de atualização (prompt de comando) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], running
- command prompt [Upgrade Advisor]
- UpgradeAdvisorWizardCmd utility
- XML formats [Upgrade Advisor]
ms.assetid: 7c83049b-9227-4723-9b7f-66288bc6bd1d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8de6913085c24f98d8305f622f5cbec31aa2a79c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058965"
---
# <a name="running-upgrade-advisor-command-prompt"></a>Executando o Supervisor de Atualização (Prompt de Comando)
  Use o utilitário **UpgradeAdvisorWizardCmd** para executar o supervisor de atualização do prompt de comando. Você pode escolher receber os resultados no formato XML ou em um arquivo CSV (valores separados por vírgula).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      UpgradeAdvisorWizardCmd [ -? ]  |   
    [ -ConfigFilefilename | <server_info> ]  
    [ -SqlUserlogin_id-SqlPasswordpassword ]  
    [ -CSV ]  
  
where <server_info> is any combination of the following:  
        -Serverserver_name-Instanceinstance_name-ASInstanceAS_instance_name-RSInstanceRS_instance_name  
```  
  
## <a name="arguments"></a>Argumentos  
 **-?**  
 Exibe a sintaxe do comando.  
  
 **-ConfigFile** _nome do arquivo_  
 É o nome do caminho e o nome do arquivo de um arquivo XML que contém as configurações a serem usadas quando você executa o utilitário **UpgradeAdvisorWizardCmd** .  
  
 *<server_info>*  
 Especifica qual computador e instância serão analisadas. Use essas opções se você não estiver usando um arquivo de configuração.  
  
 *<server_info>* pode ser qualquer combinação dos quatro argumentos a seguir:  
  
 **-Servidor** _server_name_  
 Especifica o nome do computador que será analisado. Esse computador pode ser o computador local, que é o valor padrão, ou um computador remoto.  
  
 **-Instância** _instance_name_  
 Especifica o nome da instância que será analisada. Sem valor padrão. Se você não especificar esse parâmetro, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não será verificado. O valor para uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é MSSQLSERVER. Para uma instância nomeada, use o nome da instância.  
  
 **-AS_instance_name de instância**_AS_instance_name_    
 Especifica o nome da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que será analisada. Sem valor padrão. Se você não especificar esse valor, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não será verificado. O valor para uma instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é MSSQLServerOLAPService. Para uma instância nomeada, use o nome da instância.  
  
 **-RSInstance**  _RS_instance_name_  
 Especifica o nome da instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que será analisada. Sem valor padrão. Se você não especificar esse valor, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não será verificado. O valor para uma instância padrão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é ReportServer. Para uma instância nomeada, use o nome da instância.  
  
 **-Sqluser** _login_id_  
 Se você estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse valor será o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que o Supervisor de Atualização usará para conectar-se na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você não especificar um logon, a Autenticação do Windows será usada para conectar-se na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **-** _Senha_ de senha  
 Se você usar o argumento **-sqluser** , use esse argumento para especificar a senha para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon.  
  
 **-CSV**  
 Especifica que os resultados serão fornecidos como valores separados por vírgula em um arquivo .csv, além dos resultados em XML padrão. Os resultados são gravados na pasta meus documentos \\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] upgrade Advisor\110\Reports.  
  
## <a name="return-values"></a>Valores de retorno  
 A tabela a seguir mostra os valores que **UpgradeAdvisorWizardCmd** retorna.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|A análise foi bem-sucedida e nenhum problema de atualização foi encontrado.|  
|número inteiro positivo|A análise foi bem-sucedida e foram encontrados problemas de atualização.|  
|número inteiro negativo|A análise falhou.|  
  
## <a name="remarks"></a>Comentários  
 Todas as informações necessárias para executar a análise, além dos nomes de usuários e das senhas de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], podem ser fornecidas em um arquivo de configuração XML. Esse arquivo de configuração XML é documentado no modelo. Se você não usar um arquivo de configuração, poderá analisar todos os componentes instalados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando as configurações padrão. Para isso, especifique os nomes dos computadores e das instâncias. Consulte a tabela ‘Descrições de elementos’ neste tópico para obter uma descrição das configurações do arquivo de configuração padrão.  
  
## <a name="configuration-file-template"></a>Modelo do arquivo de configuração  
 Use o seguinte XML como modelo para criar seus próprios arquivos de configuração. Você pode modificar o modelo para atender às necessidades da sua organização.  
  
```xml  
<Configuration>  
    <Server> </Server>  
    <Instance></Instance>  
    <Components>  
        <SQLServer>  
            <Databases>  
                <Database></Database>  
            </Databases>  
            <TraceFiles>  
                <TraceFile></TraceFile>  
            </TraceFiles>  
            <BatchFiles>  
                <BatchFile></BatchFile>  
            </BatchFiles>  
            <BatchSeparator></BatchSeparator>  
        </SQLServer>  
        <AnalysisServices>  
            <ASInstance></ASInstance>  
            <Databases>  
                <Database></Database>  
            </Databases>  
        </AnalysisServices>  
        <ReportingServices>  
            <RSInstance></RSInstance>  
        </ReportingServices>  
        <IntegrationServices>  
            <PackagePath></PackagePath>  
        </IntegrationServices>  
    </Components>  
</Configuration>  
```  
  
## <a name="element-descriptions"></a>Descrição do elemento  
  
|Marca|Definição|Ocorrência|  
|---------|----------------|----------------|  
|`Configuration`|Elemento pai do arquivo de configuração do Supervisor de Atualização.|Obrigatório uma vez por arquivo de configuração.|  
|`Server`|Nome do servidor que será analisado.|Opcional uma vez por arquivo de configuração. O valor padrão é o computador local.|  
|`Instance`|Nome da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que será analisada.|Opcional uma vez por arquivo de configuração. O valor padrão é a instância padrão.<br /><br /> Obrigatório uma vez por arquivo de configuração, se um elemento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou `IntegrationServices` estiver presente no servidor.|  
|`Components`|Contém elementos que especificam quais componentes serão analisados.|Obrigatório uma vez por arquivo de configuração.|  
|`SQLServer`|Contém as configurações de análise para uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].|Opcional uma vez por arquivo de configuração. Se não for especificado, os bancos de dados do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não serão analisados.|  
|`Databases` para o elemento `SQLServer`|Contém uma lista dos bancos de dados que serão analisados.|Opcional uma vez por `SQLServer` elemento. Se esse elemento não estiver presente, serão analisados todos os bancos de dados na instância.|  
|`Database` para o elemento `SQLServer`|Especifica o nome do banco de dados que será analisado.|Obrigatório uma vez ou mais se o elemento `Databases` estiver presente. Se um elemento `Database` contiver o valor "*", serão analisados todos os bancos de dados na instância. Sem valor padrão.|  
|`TraceFiles`|Contém uma lista dos arquivos de rastreamento que serão analisados.|Opcional uma vez por `SQLServer` elemento.|  
|`TraceFile`|Especifica o caminho e o nome de um arquivo de rastreamento que será analisado.|Obrigatório uma vez ou mais se o elemento `TraceFiles` estiver presente. Sem valor padrão.|  
|`BatchFiles`|Contém uma lista dos arquivos em lotes que serão analisados.|Opcional uma vez por `SQLServer` elemento.|  
|`BatchFile`|Especifica um arquivo em lote que será analisado. Podem ser vários.|Obrigatório uma vez ou mais se o elemento `BatchFiles` estiver presente. Sem valor padrão.|  
|`BatchSeparator`|Especifica o separador de lote usado em seus arquivos em lotes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Opcional uma vez por `SQLServer` elemento. O valor padrão é GO.|  
|`AnalysisServices`|Contém configurações de análise do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|Opcional uma vez por arquivo de configuração. Se não for especificado, os bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não serão analisados.|  
|`ASInstance`|Especifica o nome de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|Obrigatório uma vez por elemento `AnalysisServices`. Sem valor padrão.|  
|`Databases` para o elemento `Analysis Services`|Contém uma lista dos bancos de dados que serão analisados.|Opcional uma vez por `AnalysisServices` elemento. Se esse elemento não estiver presente, serão analisados todos os bancos de dados na instância.|  
|`Database` para o elemento `AnalysisServices`|Especifica o nome do banco de dados que será analisado.|Obrigatório uma vez ou mais se o elemento `Databases` estiver presente. Se um elemento `Database` contiver o valor "*", serão analisados todos os bancos de dados na instância. Sem valor padrão.|  
|`ReportingServices`|Especifica que a análise será executada no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|Opcional uma vez por arquivo de configuração. Se não for especificado, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não será analisado.|  
|`RSInstance`|Especifica o nome de uma instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Obrigatório uma vez por elemento `ReportingServices`. Sem valor padrão.|  
|`IntegrationServices`|Contém configurações de análise do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|Opcional uma vez por arquivo de configuração. Se não for especificado, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não será analisado.|  
|`PackagePath`|Especifica o caminho de um conjunto de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|Opcional uma vez por `IntegrationServices` elemento. Se esse elemento não estiver presente, a análise ocorrerá na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e nenhum pacote armazenado externamente será analisado. Sem valor padrão.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-run-upgrade-advisor-using-a-configuration-file"></a>a. Executar o Supervisor de Atualização usando um arquivo de configuração  
 O exemplo a seguir mostra como executar o Supervisor de Atualização a partir do prompt de comando usando um arquivo de configuração que especifica o que deve ser analisado. Este exemplo usa a Autenticação do Windows para conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"  
```  
  
### <a name="b-run-upgrade-advisor-using-default-configuration-settings"></a>B. Executar o Supervisor de Autenticação usando definições de configuração padrão  
 O exemplo a seguir mostra como executar o Supervisor de Atualização a partir do prompt de comando usando definições de configuração padrão e a Autenticação do Windows.  
  
```  
UpgradeAdvisorWizardCmd -Server MyServer -Instance MyInst   
```  
  
### <a name="c-run-upgrade-advisor-using-ssnoversion-authentication"></a>C. Executar o Supervisor de Atualização usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O exemplo a seguir mostra como executar o Supervisor de Atualização a partir do prompt de comando usando um arquivo de configuração. Este exemplo especifica um nome de usuário e uma senha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"   
    -SqlUser "MyUserName" -SqlPassword "QweRTy-55"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Resolvendo problemas de atualização](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Trabalhando com o supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Executando o supervisor de atualização &#40;a interface do usuário&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)  
  
  
