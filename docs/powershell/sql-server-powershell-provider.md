---
title: Provedor do SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: powershell
ms.component: powershell
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], provider
- PowerShell [SQL Server], SQL Server PowerShell Provider
- Providers [PowerShell]
- SMO [SQL Server], PowerShell
- PowerShell [SQL Server], SMO
- SQL Server Management Objects, PowerShell
ms.assetid: b97acc43-fcd2-4ae5-b218-e183bab916f9
caps.latest.revision: 61
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0d4b699045824f5a2563dc4973b94a1b091ce7b5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-powershell-provider"></a>SQL Server PowerShell Provider
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

O provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para o Windows PowerShell expõe a hierarquia de objetos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em caminhos semelhantes aos caminhos do sistema de arquivos. Você pode usar os caminhos para localizar um objeto e usar os métodos dos modelos SMO ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Object) para executar ações nos objetos.  
  
> [!NOTE]
> Há dois módulos do SQL Server PowerShell; **SqlServer** e **SQLPS**. O módulo **SQLPS** está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está sendo atualizado. O módulo do PowerShell mais atualizado é o módulo do **SqlServer**. O módulo do **SqlServer** contém versões atualizadas dos cmdlets no **SQLPS** e também inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL.  
> As versões anteriores do módulo do **SqlServer** *foram* incluídas no SQL Server Management Studio (SSMS), mas apenas nas versões 16.x do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões posteriores, o módulo do **SqlServer** deve ser instalado da Galeria do PowerShell.
> Para instalar o módulo do **SqlServer**, consulte [Instalar o SQL Server PowerShell](download-sql-server-ps-module.md).


## <a name="benefits-of-the-sql-server-powershell-provider"></a>Benefícios do provedor do SQL Server PowerShell  
 Os caminhos implementados pelo provedor [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] habilitam a análise fácil e interativa de todos os objetos em uma instância do SQL Server. Você pode navegar nos caminhos usando aliases do Windows PowerShell semelhantes aos comandos usados para navegar em caminhos do sistema de arquivos.  
  
## <a name="the-sql-server-powershell-hierarchy"></a>A hierarquia do SQL Server PowerShell  
 Os produtos cujos modelos de objetos ou de dados podem ser representados em uma hierarquia usam os provedores do Windows PowerShell para expor as hierarquias. A hierarquia é exposta usando uma estrutura de unidades e caminhos semelhante à usada pelo sistema de arquivos do Windows.  
  
 Cada provedor do Windows PowerShell implementa uma ou mais unidades. Cada unidade é o nó raiz de uma hierarquia de objetos relacionados. O provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] implementa uma unidade SQLSERVER:. O provedor também define um conjunto de pastas primárias para a unidade SQLSERVER:. Cada pasta e suas respectivas subpastas representam o conjunto de objetos que podem ser acessados usando um modelo de objeto de gerenciamento do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Quando o foco é uma subpasta em um caminho que começa com uma dessas pastas primárias, você pode usar os métodos do modelo de objeto associado para executar ações com o objeto representado pelo nó. As pastas do Windows PowerShell implementadas pelo provedor do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] estão listadas na tabela a seguir:  
  
|Pasta|Namespace do modelo de objeto do SQL Server|Objetos|  
|------------|---------------------------------------|-------------|  
|SQLSERVER:\SQL|<xref:Microsoft.SqlServer.Management.Smo><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Agent><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Broker><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Mail>|Objetos do banco de dados, como tabelas, exibições e procedimentos armazenados.|  
|SQLSERVER:\SQLPolicy|<xref:Microsoft.SqlServer.Management.Dmf><br /><br /> <xref:Microsoft.SqlServer.Management.Facets>|Objetos de gerenciamento baseado em políticas, como políticas e facetas.|  
|SQLSERVER:\SQLRegistration|<xref:Microsoft.SqlServer.Management.RegisteredServers><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>|Objetos de servidor registrados, como grupos de servidores e servidores registrados.|  
|SQLSERVER:\Utility|<xref:Microsoft.SqlServer.Management.Utility>|Objetos de utilitário, como instâncias gerenciadas do [!INCLUDE[ssDE](../includes/ssde-md.md)].|  
|SQLSERVER:\DAC|<xref:Microsoft.SqlServer.Management.DAC>|Objetos de aplicativo da camada de dados como pacotes do DAC e operações como implantação de um DAC.|  
|SQLSERVER:\DataCollection|<xref:Microsoft.SqlServer.Management.Collector>|Objetos de coletor de dados, como conjuntos de coleta e repositórios de configuração.|  
|SQLSERVER:\IntegrationServices|<xref:Microsoft.SqlServer.Management.IntegrationServices>|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] objetos como projetos, pacotes e ambientes.|  
|SQLSERVER:\SQLAS|<xref:Microsoft.AnalysisServices>|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] objetos como cubos, agregações e dimensões.|  
  
 Por exemplo, você pode usar a pasta SQLSERVER:\SQL para iniciar caminhos que podem representar qualquer objeto com suporte pelo modelo de objeto do SMO. A parte à esquerda de um caminho SQLSERVER:\SQL é SQLSERVER:\SQL\\*ComputerName*\\*InstanceName*. Os nós após o nome da instância alternam entre coleções de objetos (como *Bancos de Dados* ou *Exibições*) e nomes de objetos (como AdventureWorks2012). Os esquemas não são representados como classes de objetos. Ao especificar o nó para um objeto de alto nível em um esquema, como uma tabela ou exibição, é preciso especificar o nome do objeto no formato *SchemaName.ObjectName*.  
  
 O seguinte exemplo mostra o caminho da tabela Vendor no esquema Purchasing do banco de dados AdventureWorks2012 em uma instância padrão do [!INCLUDE[ssDE](../includes/ssde-md.md)] no computador local:  
  
```  
SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables\Purchasing.Vendor  
```  
  
 Para obter mais informações sobre a hierarquia de modelos de objeto do SMO, veja [Diagrama de modelos de objetos SMO](../relational-databases/server-management-objects-smo/smo-object-model-diagram.md).  
  
 Os nós de coleção em um caminho são associados a uma classe de coleção no modelo de objeto associado. Os nós de nomes de objetos são associados a uma classe de objeto no modelo de objeto associado, como na tabela a seguir:  
  
|Caminho|Classe do SMO|  
|----------|---------------|  
|SQLSERVER:\SQL\MyComputer\DEFAULT\Databases|<xref:Microsoft.SqlServer.Management.Smo.DatabaseCollection>|  
|SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012|<xref:Microsoft.SqlServer.Management.Smo.Database>|  
  
## <a name="sql-server-provider-tasks"></a>Tarefas de provedor SQL Server  
  
|Descrição da tarefa|Artigo|  
|----------------------|-----------|  
|Descreve como usar cmdlets do Windows PowerShell para navegar pelos nós em um caminho, e a cada nó obtém uma lista dos objetos desse nó.|[Navegar em caminhos do SQL Server PowerShell](navigate-sql-server-powershell-paths.md)|  
|Descreve como usar os métodos e propriedades do SMO para relatar e executar trabalho no objeto representado por um nó em um caminho. Também descreve como obter uma lista dos métodos e propriedades do SMO para esse nó.|[Trabalhar com caminhos do SQL Server PowerShell](work-with-sql-server-powershell-paths.md)|  
|Descreve como converter um URN (Nome de Recurso Uniforme) de SMO em um caminho de provedor SQL Server.|[Converter URNs em caminhos de provedor SQL Server](https://docs.microsoft.com/powershell/module/sqlserver/Convert-UrnToPath)|  
|Descreve como abrir conexões de Autenticação do SQL Server usando o provedor [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Por padrão, o provedor usa as conexões de Autenticação do Windows feitas usando as credenciais da conta Windows que executam a sessão do Windows PowerShell.|[Gerenciar a autenticação no PowerShell do Mecanismo de Banco de Dados](manage-authentication-in-database-engine-powershell.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
