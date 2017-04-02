---
title: "PowerShell scripting in Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
caps.latest.revision: 44
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 44
---
# PowerShell scripting in Analysis Services
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] inclui componentes do PowerShell para navegar, administrar e consultar o servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], objetos multidimensionais e de tabela no PowerShell:  
  
-   O provedor **SQLAS**, usado para navegação da hierarquia de objetos, está disponível quando você tem qualquer instância local do Analysis Services (o modo do servidor é irrelevante).  
  
-   O módulo **SQLASCMDLETS** fornece cmdlets específicos para tarefas, como fazer backup, restaurar, processar, bem como o [cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) de uso geral que aceita qualquer consulta ASSL/XMLA ou Linguagem de Script de Modelo de Tabela (TMSL) ou arquivo de entrada de script.  
  
 Os dois componentes implementam um subconjunto da interface administrativa do Objeto de Gerenciamento do Analysis Services ([Microsoft.AnalysisServices Namespace](http://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx)), fornecendo cmdlets para gerenciar e criar objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  Ambos são extensões do módulo raiz do **SQLPS** para o SQL Server. Para usar os componentes do PowerShell do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você deve começar importando o **SQLPS**. A sintaxe e os exemplos de todos os cmdlets podem ser encontrados em [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md).  Para ver um exemplo de como usar os tipos de AMO no PowerShell para criar um Banco de dados de tabela, veja [AMO PowerShell Example](../../analysis-services/powershell/amo-powershell-example.md).  
  
##  <a name="bkmk_prereq"></a> Etapa 1: Instalar os componentes do PowerShell  
 A abordagem recomendada para obter componentes do PowerShell é instalar o SQL Server Management Studio (SSMS). Essa abordagem fornece os módulos do PowerShell para SQL Server e o provedor de dados de Gerenciamento do Analysis Services (AMO). Ter o SSMS também oferece uma ferramenta para gerar com facilidade entradas de XMLA e TMSL a serem usadas no seu script do PowerShell.  
  
 Considere a instalação de uma instância local do Analysis Services. Uma instância local permite a navegação da hierarquia do objeto por meio do provedor do **SQLAS** , mesmo se você nunca usá-lo para hospedar um banco de dados.  
  
1.  Vá para  [Baixar o SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/mt238290.aspx) para obter a versão mais recente do Management Studio. A versão mais recente do Management Studio. inclui um AMO atualizado que oferece suporte a definições de objeto de metadados de tabela, para modelos de Tabela criados no nível de compatibilidade 1200.  
  
2.  Depois de instalar o Management Studio, abra uma janela do PowerShell. Não precisa ser uma janela de administrador.  
  
3.  Digite `Get-Module -ListAvailable` para confirmar se os módulos **SQLPS** e **SQLASCMDLETS** aparecem na lista.  
  
     Você não verá o **SQLAS** a menos que você também instale uma instância local do Analysis Services (seja no modo de Tabela ou Multidimensional).  
  
4.  Digite `Get-Command -Module sqlascmdlets` para produzir uma lista dos cmdlets usados na administração do Analysis Services.  
  
     Os**SQLASCMDLETS** estão disponíveis mesmo quando o provedor do **SQLAS** está ausente.  
  
    -   [Cmdlet Add-RoleMember](../../analysis-services/powershell/add-rolemember-cmdlet.md)  
  
    -   [Cmdlet Backup-ASDatabase](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)  
  
    -   [Cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) **-inputfile**  
  
    -   [Chamar ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)  
  
    -   [Cmdlet ProcessCube](../../analysis-services/powershell/invoke-processcube-cmdlet.md)  
  
    -   [Cmdlet Invoke-ProcessDimension](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)  
  
    -   [Cmdlet Invoke-ProcessPartition](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)  
  
    -   [Cmdlet Invoke-ProcessTable](../../analysis-services/powershell/invoke-processtable-cmdlet.md)  
  
    -   [Cmdlet Merge-Partition](../../analysis-services/powershell/merge-partition-cmdlet.md)  
  
    -   [Cmdlet New-RestoreFolder](../../analysis-services/powershell/new-restorefolder-cmdlet.md)  
  
    -   [Cmdlet New-RestoreLocation](../../analysis-services/powershell/new-restorelocation-cmdlet.md)  
  
    -   [Cmdlet Remove-RoleMember](../../analysis-services/powershell/remove-rolemember-cmdlet.md)  
  
    -   [Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)  
  
> [!NOTE]  
>  O Windows PowerShell é instalado por padrão em versões mais recentes dos sistemas operacionais Windows. A recomendação é 4.0 ou posterior.  
  
## Etapa 2: Carregar componentes para iniciar uma sessão interativa  
 Depois que os componentes estão instalados, o carregamento deles inicia uma sessão interativa.  
  
1.  Digitar `Import-Module sqlps -DisableNameChecking`,  
  
     Carrega os componentes do SQL Server PowerShell, incluindo aquelas para o Analysis Services, e suprime o aviso sobre nomes de verbos inválidos.  
  
2.  Digite `sqlserver:`  
  
     Você verá o prompt mudar para **PS SQLSERVER:\\>**.  
  
3.  Se o Analysis Services estiver instalado localmente, você poderá navegar na hierarquia de objeto. Digite `cd sqlas` para abrir o provedor do **SQLAS**.  
  
4.  Digite `dir` para listar as instâncias do Analysis Services. O provedor não faz distinção entre as instâncias de tabela e multidimensionais.  
  
## Permissões  
 Uma sessão interativa do PowerShell é executada sob a identidade de segurança da pessoa que a inicia. A maioria das tarefas exige que a pessoa que está iniciando a sessão também seja um administrador do servidor do Analysis Services.  
  
 As tarefas agendadas do PowerShell devem ser consideradas operações autônomas. A conta que está executando o agendador, como o serviço do SQL Server Agent, provavelmente precisa ser um administrador do Analysis Services (dependendo da tarefa).  
  
 As pastas de dados locais, como os diretórios de backup e dados padrão, já estão configuradas com permissões de sistema de arquivos que permitem a uma instância local ler e gravar nesses locais.  
  
 A administração remota, especialmente quando realizada de computadores cliente que não possuem o Analysis Services instalado, requer que a instância remota do servidor do Analysis Services que está executando a ação tenha permissões do sistema do arquivo para ler arquivos durante a restauração ou gravar arquivos durante o backup.  
  
## Arquivos de entrada do script: ASSL/XMLA ou TMSL  
 Se você estiver usando **invoke-ascmd** para executar o script, o modo de servidor, o tipo de banco de dados e o nível de compatibilidade serão fatorados em como construir o script.  
  
-   Os bancos de dados multidimensionais e de tabela nos níveis de compatibilidade 1050-1103 respondem a scripts gravados em XMLA (usando as extensões ASSL específicas para definições de objeto do Analysis Services).  
  
-   Os bancos de dados de tabela no SQL Server 2016 (nível de compatibilidade 1200) respondem ao script TMSL.  
  
 Se você estiver trabalhando com versões mistas de modelos de Tabela na mesma instância do SQL Server 2016, lembre-se de usar o script certo.  
  
> [!NOTE]  
>  Os scripts podem ser gerados no SQL Server Management Studio e depois modificados conforme necessário. Os bancos de dados de tabela no nível de compatibilidade 1200 têm scripts em TMSL. Todos os outros têm scripts em XMLA/ASSL. Uma instância do SQL Server 2016 no modo de Tabela oferece suporte a ambas as linguagens de script.  
  
## Administração local e remota  
 A administração local do Analysis Services por meio de comandos e scripts do PowerShell é mais fácil por dois motivos:  
  
-   Permite o uso do provedor do **SQLAS** para navegar na hierarquia do objeto.  
  
-   As permissões de arquivos que habilitam o Analysis Services a fazer a leitura de pastas de dados padrão, como para tarefas de backup e restauração, já estão em vigor, supondo que você esteja usando essas pastas como o local do banco de dados, e a instância do servidor local seja usada para a operação.  
  
 O gerenciamento de uma instância remota requer configuração adicional. As etapas a seguir pressupõem que você concluiu as etapas de instalação do Management Studio, mas que a instância de serviço está em um computador remoto. Você deve ter direitos de administrador no servidor do Analysis Services.  
  
 Como o Analysis Services é remoto, não há nenhum provedor do **SQLAS** para a navegação local da hierarquia do objeto. Se você estiver restaurando arquivos de uma pasta local em vez de uma instância do Analysis Services, será preciso criar compartilhamentos e conceder ao servidor acesso de leitura para os arquivos.  
  
1.  Abra uma janela do PowerShell de administrador.  
  
2.  Digite `Set-ExecutionPolicy RemoteUnsigned`  
  
3.  No Explorador de Arquivos, verifique se todos as pastas que contêm arquivos de dados estão sendo compartilhadas, e se a instância do Analysis Services tem permissões de leitura para o conteúdo.  
  
##  <a name="bkmk_vers"></a> Versões e modos compatíveis do Analysis Services  
 A tabela a seguir mostra a disponibilidade do Analysis Services PowerShell em diferentes contextos.  
  
|Contexto|Disponibilidade de recursos do PowerShell|  
|-------------|-------------------------------------|  
|Instâncias e bancos de dados multidimensionais|Com suporte para administração local e remota.<br /><br /> A partição de mesclagem exige uma conexão local.|  
|Instâncias e bancos de dados tabulares|Com suporte para administração local e remota, em todos os níveis de compatibilidade.<br /><br /> Os cmdlets SQLAS para modelos de Tabela no nível de compatibilidade 1200 usando a Linguagem de Script de Modelo de Tabela (TMSL) em JSON em vez de XMLA.|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|Suporte limitado. É possível usar conexões HTTP e o provedor SQLAS para visualizar informações da instância e do banco de dados.<br /><br /> Porém, não há suporte para usar os cmdlets. Você não pode usar o PowerShell para Analysis Services para fazer backup e restauração de um banco de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] na memória, nem deve adicionar ou remover funções, processar os dados ou executar script XMLA arbitrário.<br /><br /> Para fins de configuração, o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint tem suporte interno ao PowerShell que é fornecido separadamente. Para obter mais informações, consulte [Referência do PowerShell para Power Pivot para SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md).|  
|Conexões nativas a cubos locais<br /><br /> “Data Source=c:\backup\test.cub”|Sem suporte.|  
|Conexões HTTP a arquivos de conexão do modelo semântico BI (.bism) no SharePoint<br /><br /> “Data Source=http://server/shared_docs/name.bism”|Sem suporte.|  
|Conexões inseridas em bancos de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> “Data Source=$Embedded$”|Sem suporte.|  
|Contexto de servidor local em procedimentos armazenados do Analysis Services<br /><br /> “Data Source=*”|Sem suporte.|  
  
## Exemplos de tarefas de administração do servidor com o PowerShell  
 **Listar as propriedades de servidor**  
  
 As propriedades do servidor são expostas de várias maneiras.  Caso esteja familiarizado com as propriedades expostas no msmdsrv. ini ou nas páginas de propriedade do Management Studio, você verá nos exemplos abaixo que as propriedades são, na verdade, retornadas de objetos diferentes.  
  
 Este script carrega um objeto do Servidor AMO. Se você precisar de um nome de propriedade totalmente qualificado, é possível executar esse script para retornar a lista.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$as.serverproperties  
  
```  
  
 Esse script retorna propriedades e métodos no nível de instância. Nesta lista, você pode ler valores como **ServerMode**, **Version**, **ProductName**ou **ProductLevel**.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as | get-member  
  
```  
  
 **Obter o modo servidor**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.ServerMode  
```  
  
 **Obter o nível de compatibilidade padrão**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.DefaultCompatibilityLevel  
```  
  
 **Obter uma lista de bancos de dados**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.databases  
```  
  
 **Alterar o número da porta**  
  
 Esse script cria um objeto para uma instância nomeada, declara a porta, define a porta, atualiza a instância do servidor, desconecta o objeto e reinicia o serviço. Como uma etapa de verificação, você pode abrir uma nova conexão e retornar a porta.  
  
 Você também pode verificar a porta no arquivo msmdsrv.ini ou na página de propriedades Geral do servidor no Management Studio.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$port = $as.serverproperties['Port']  
$port | select *  
$port.Value = [int]55555  
$as.Update()  
$as.Disconnect()  
restart-service 'MSOLAP$TABULAR'  
$as.connect("server-name\instance-name")  
$port | select *  
  
```  
  
## Consulte também  
 [Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Instalar o SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)   
 [Gerenciar modelos tabulares usando o PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)   
 [Configurar o acesso HTTP ao Analysis Services no IIS &#40;(Serviços de Informações da Internet)&#41; 8.0](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md)  
  
  