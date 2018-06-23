---
title: cmdlet Invoke-PolicyEvaluation | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, Invoke-PolicyEvaluation
- Policy-Based Management, PowerShell
- Invoke-PolicyEvaluation cmdlet
- Cmdlets [SQL Server], Invoke-PolicyEvaluation
- PowerShell [SQL Server], Invoke-PolicyEvaluation
ms.assetid: 3e6d4f5a-59b7-4203-b95a-f7e692c0f131
caps.latest.revision: 18
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: c0ec56b9cde0a2def994d8deffd0ef051459dbf7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006697"
---
# <a name="invoke-policyevaluation-cmdlet"></a>cmdlet Invoke-PolicyEvaluation
  O**Invoke-PolicyEvaluation** é um cmdlet do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que relata se um conjunto de objetos SQL Server de destino é compatível com as condições especificadas em uma ou mais políticas do Gerenciamento Baseado em Políticas.  
  
## <a name="using-invoke-policyevaluation"></a>Usando Invoke-PolicyEvaluation  
 O**Invoke-PolicyEvaluation** avalia uma ou mais políticas em relação a um conjunto de objetos SQL Server, chamado conjunto de destino. O conjunto de objetos de destino origina-se em um servidor de destino. Cada política define condições, as quais são os estados permitidos dos objetos de destino. Por exemplo, a política **Banco de Dados Confiável** declara que a propriedade TRUSTWORTHY do banco de dados deve ser definida como OFF.  
  
 O parâmetro **-AdHocPolicyEvaluationMode** especifica as ações tomadas:  
  
 Verificar  
 Relate o status de conformidade dos objetos de destino que usam as credenciais do seu logon atual. Não reconfigure nenhum objeto. Essa é a configuração padrão.  
  
 CheckSqlScriptAsProxy  
 Relate o status de conformidade dos objetos de destino que usam as credenciais do logon de proxy **##MS_PolicyTSQLExecutionLogin##** . Não reconfigure nenhum objeto.  
  
 Configurar  
 Relate o status de conformidade dos objetos de destino que usam as credenciais do seu logon atual. Reconfigure qualquer opção definível e determinística que não estejam em conformidade com as políticas.  
  
## <a name="specifying-polices"></a>Especificando políticas  
 A forma como você especifica uma política depende de onde ela está armazenada. As políticas podem ser armazenadas em dois formatos:  
  
-   Elas podem ser objetos armazenados em um repositório de política, como, por exemplo, uma instância do Mecanismo do Banco de Dados. Você pode usar a pasta SQLSERVER:\SQLPolicy para especificar o local de políticas em um repositório de políticas. Você pode usar cmdlets Windows PowerShell para filtrar as diretivas de entrada com base em suas propriedades, como, por exemplo, o uso de Where-Object para filtrar na categoria da diretiva ou Get-Item para filtrar no nome da diretiva.  
  
-   Eles podem ser exportados como arquivos XML. Você pode usar uma unidade de sistema de arquivos, por exemplo D:, para especificar o local dos arquivos XML. Você pode usar cmdlets Windows PowerShell, por exemplo Where-Object, para filtrar as diretivas nas propriedades de arquivo, como, por exemplo, nome de arquivo.  
  
 Se as políticas estiverem armazenadas em um repositório de políticas, você deverá passar um conjunto de PSObjects que aponte para as políticas a serem avaliadas. Em geral, isso é feito indicando a saída de um cmdlet, por exemplo, Get-Item para **Invoke-PolicyEvaluation**e não exige que você especifique o parâmetro **-Policy** . Por exemplo, se você importou as políticas do Microsoft Best Practices para sua instância do mecanismo de banco de dados, esse comando avalia a política **Status do Banco de Dados** :  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Get-Item "Database Status" | Invoke-PolicyEvaluation -TargetServerName "MYCOMPUTER"  
```  
  
 Este exemplo mostra o uso de Where-Object para filtrar várias políticas de um repositório de políticas com base na propriedade **PolicyCategory** . Os objetos da saída indicada de **Where-Object** são consumidos por **Invoke-PolicyEvaluation**.  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
gci | Where-Object {$_.PolicyCategory -eq "Microsoft Best Practices: Maintenance"} | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
 Se as políticas forem armazenadas como arquivos XML, use o parâmetro **-Policy** para fornecer o caminho e o nome de cada política. Se você não especificar um caminho no parâmetro **-Policy** , **Invoke-PolicyEvaulation** usará a configuração atual do caminho **sqlps** . Por exemplo, este comando avalia uma das políticas do Microsoft Best Practice instaladas com SQL Server no banco de dados padrão para seu logon:  
  
```  
Invoke-PolicyEvaluation -Policy "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033\Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 Esse comando faz a mesma coisa, apenas usa o caminho **sqlps** atual para estabelecer o local do arquivo XML da política:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 Esse exemplo mostra o uso do cmdlet **Get-ChildItem** para recuperar vários arquivos XML de políticas e indicar os objetos em **Invoke-PolicyEvaluation**:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
gci "Database Status.xml", "Trustworthy Database.xml" | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
## <a name="specifying-the-target-set"></a>Especificando o conjunto de destino  
 Use três parâmetros para especificar o conjunto de objetos de destino:  
  
-   O **-TargetServerName** especifica a instância do SQL Server que contém os objetos de destino. Você pode especificar as informações em uma cadeia de caracteres que use o formato definido para a propriedade ConnectionString da classe <xref:System.Data.SqlClient.SqlConnection> . Você pode usar a classe <xref:System.Data.SqlClient.SqlConnectionStringBuilder> para criar uma cadeia de conexão formatada corretamente. Você pode criar também um objeto <xref:Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection> e transmiti-lo para **-TargetServer**. Se você fornecer uma cadeia de caracteres que tenha apenas o nome do servidor, **Invoke-PolicyEvaluation** usará a Autenticação do Windows para se conectar ao servidor.  
  
-   O **-TargetObjects** utiliza um objeto ou uma matriz de objetos que representam os objetos SQL Server no conjunto de destino. Por exemplo, você pode criar uma matriz de objetos da classe <xref:Microsoft.SqlServer.Management.Smo.Database> para transmitir para **-TargetObjects**.  
  
-   O **-TargetExpressions** utiliza uma cadeia de caracteres que contém uma expressão de consulta que especifica os objetos no conjunto de destino. A expressão de consulta está na forma de nós separados pelo caractere '/'. Cada nó está na forma ObjectType[Filtro]. O tipo do objeto é um dos objetos em uma hierarquia de objetos SQL Server Management Object (SMO). O filtro é uma expressão que filtra objetos desse nó. Para obter mais informações, consulte [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md).  
  
 Especifique **-TargetObjects** ou **-TargetExpression**, mas não ambos.  
  
 Este exemplo usa um objeto Sfc.SqlStoreConnection para especificar o servidor de destino:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
$conn = New-Object Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection("server='MYCOMPUTER';Trusted_Connection=True")  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName $conn  
```  
  
 Este exemplo usa **-TargetExpression** para identificar o banco de dados específico a avaliar:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MyComputer" -TargetExpression "Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']"  
```  
  
## <a name="evaluating-analysis-services-policies"></a>Avaliando políticas do Analysis Services  
 Para avaliar as políticas com base em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], carregue e registre um assembly no PowerShell, crie uma variável com o objeto de conexão do Analysis Services e passe a variável para o parâmetro **-TargetObject** . Este exemplo mostra como avaliar a política de configuração da área da superfície das Práticas Recomendadas para o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\AnalysisServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices")  
$SSASsvr = new-object Microsoft.AnalysisServices.Server  
$SSASsvr.Connect("Data Source=Localhost")  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Analysis Services Features.xml" -TargetObject $SSASsvr  
```  
  
## <a name="evaluating-reporting-services-policies"></a>Avaliando políticas do Reporting Services  
 Para avaliar as políticas do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , carregue e registre um assembly no PowerShell, crie uma variável com um objeto de conexão do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e passe a variável para o parâmetro **-TargetObject** . Este exemplo mostra como avaliar a política de configuração da área da superfície das Práticas Recomendadas para o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\ReportingServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Dmf.Adapters")  
$SSRSsvr = new-object Microsoft.SqlServer.Management.Adapters.RSContainer('MyComputer')  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Reporting Services 2008 Features.xml" -TargetObject $SSRSsvr  
```  
  
## <a name="formatting-output"></a>Formatando a saída  
 Por padrão, a saída de **Invoke-PolicyEvaluation** é exibida na janela do prompt de comando como um relatório conciso em formato legível. Você pode usar o parâmetro **-OutputXML** para especificar que, em vez disso, o cmdlet deve produzir um relatório detalhado como um arquivo XML. **Invoke-PolicyEvaluation** usa o esquema SML-IF (Systems Modeling Language Interchange Format) para que o arquivo possa ser lido por leitores de SML-IF.  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Invoke-PolicyEvaluation -Policy "Datbase Status" -TargetServer "MYCOMPUTER" -OutputXML > C:\MyReports\DatabaseStatusReport.xml  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usar cmdlets do Mecanismo de Banco de Dados](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  