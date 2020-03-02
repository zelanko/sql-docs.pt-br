---
title: Tipo de conexão Oracle (Construtor de Relatórios e Servidor de Relatórios do Power BI) | Microsoft Docs
ms.date: 02/26/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 9db86dd2-beda-42d8-8af7-2629d58a8e3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 216ab9a4d5dcfe18fe6346eadeec8778415cdeb4
ms.sourcegitcommit: 1035d11c9fb7905a012429ee80dd5b9d00d9b03c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/26/2020
ms.locfileid: "77634835"
---
# <a name="oracle-connection-type-report-builder--power-bi-report-server--microsoft-docs"></a>Tipo de conexão Oracle (Construtor de Relatórios e Servidor de Relatórios do Power BI | Microsoft Docs)

Para usar dados de um banco de dados Oracle no seu relatório, é necessário ter um conjunto de dados baseado na fonte de dados do relatório do tipo Oracle. Esse tipo de fonte de dados interno usa o Provedor de Dados Oracle diretamente e exige um componente do software cliente Oracle. Este artigo explica como baixar e instalar drivers para o Reporting Services, o Servidor de Relatórios do Power BI e o Construtor de Relatórios.

## <a name="64-bit-drivers-for-the-report-servers"></a>Drivers de 64 bits para os servidores de relatório

O Servidor de Relatórios do Power BI e o SQL Server Reporting Services 2016 e 2017 usam o ODP.NET Gerenciado. As etapas a seguir só são necessárias ao usar os drivers 18x mais recentes. Elas supõem que você tenha instalado os arquivos em c:\oracle64.

1. No site de download da Oracle, instale o [OUI (Instalador Universal Oracle) ODAC de 64 bits da Oracle](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdeploy-4242173.html). 
2. Registre o cliente gerenciado ODP.NET no GAC:  C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
3. Adicione entradas do cliente gerenciado ODP.NET a machine.config:  C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odpm /frameworkversion:v4.0.30319 /productversion:4.122.18.3

### <a name="power-bi-reports-use-unmanaged-odpnet"></a>Os relatórios do Power BI usam o ODP.NET Não Gerenciado

Os relatórios do Power BI usam o **ODP.NET Não Gerenciado**. Siga estas etapas para registrar o ODP.NET Não Gerenciado:

1. Registre o cliente não gerenciado ODP.NET no GAC:

   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
2. Adicione entradas de cliente não gerenciado ODP.NET a machine.config:

   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odp /frameworkversion:v4.0.30319 /productversion:4.122.18.3
 
## <a name="32-bit-drivers-for-report-builder"></a>Drivers de 32 bits para o Construtor de Relatórios

As etapas a seguir só são necessárias ao usar os drivers 18x mais recentes. Elas supõem que você tenha instalado os arquivos em c:\oracle32.

1. No site de download da Oracle, instale o [OUI (Instalador Universal Oracle) ODAC de 32 bits da Oracle](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdev-4242174.html).
2. Registre o cliente gerenciado ODP.NET no GAC:  C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
3. Adicione entradas do cliente gerenciado ODP.NET a machine.config:  C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odpm /frameworkversion:v4.0.30319 /productversion:4.122.18.3

### <a name="power-bi-reports-use-unmanaged-odpnet"></a>Os relatórios do Power BI usam o ODP.NET Não Gerenciado  

Os relatórios do Power BI usam o **ODP.NET Não Gerenciado**. Siga estas etapas para registrar o ODP.NET Não Gerenciado:

1. Registre o cliente não gerenciado ODP.NET no GAC:

   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
2. Adicione entradas de cliente não gerenciado ODP.NET a machine.config:

   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odp /frameworkversion:v4.0.30319 /productversion:4.122.18.3
 

 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 Contate o administrador do banco de dados para obter informações sobre a conexão e as credenciais que devem ser usadas para se conectar à fonte de dados. O exemplo de cadeia de conexão a seguir especifica um banco de dados Oracle no servidor chamado "Oracle18" com Unicode. O nome do servidor deve coincidir com o que está definido no arquivo de configuração Tnsnames.ora como o nome da instância do servidor Oracle.  
  
```  
Data Source="Oracle"; Unicode="True"  
```  
  
 Para ver mais exemplos de cadeias de conexão, confira [Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
##  <a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Para obter mais informações, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](specify-credential-and-connection-information-for-report-data-sources.md).  
  
  
##  <a name="Query"></a> Consultas  
 Para criar um conjunto de dados, você pode selecionar um procedimento armazenado na lista suspensa ou criar uma consulta SQL. Para criar uma consulta, use o designer de consulta baseado em texto. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas Baseadas em Texto &#40;Construtor de Relatórios&#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
 É possível especificar procedimentos armazenados que retornem apenas um conjunto de resultados. Não há suporte para o uso de consultas baseadas em cursor.  
  
##  <a name="Parameters"></a> Parâmetros  
 Se a consulta incluir variáveis de consulta, os parâmetros de relatório correspondentes serão gerados automaticamente. Essa extensão dá suporte a parâmetros nomeados. Para o Oracle versão 9 ou posterior, há suporte para parâmetros de vários valores.  
  
 Os parâmetros de relatório são criados com valores de propriedade padrão que talvez precisem ser modificados. Por exemplo, cada parâmetro de relatório é do tipo de dados **Texto**. Depois que os parâmetros de relatório forem criados, talvez seja necessário alterar os valores padrão. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Remarks"></a> Comentários  
 Para que você possa se conectar a uma fonte de dados Oracle, o administrador do sistema deve ter instalado a versão do .NET Data Provider for Oracle que dê suporte à recuperação de dados do banco de dados Oracle. O provedor de dados deve ser instalado no mesmo computador que o Construtor de Relatórios e também no servidor de relatório.  
  
 Para obter mais informações, consulte os seguintes artigos:  
  
-   [Como usar o Reporting Services para configurar e acessar uma fonte de dados Oracle](https://docs.microsoft.com/archive/blogs/dataaccesstechnologies/configure-oracle-data-source-for-sql-server-reporting-services-ssdt-and-report-server)  
-   [Como adicionar permissões à entidade de segurança de NETWORK SERVICE](https://support.microsoft.com/kb/870668)  
  
### <a name="alternate-data-extensions"></a>Extensões de dados alternativas 
 
 Você também pode recuperar dados de um banco de dados Oracle com o uso de um tipo de fonte de dados OLE DB. Para obter mais informações, consulte [Tipo de conexão OLE DB &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md).  

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions" 
### <a name="report-models"></a>Modelos de relatório  

 Também é possível criar modelos com base em um banco de dados Oracle.  
::: moniker-end
   
### <a name="platform-and-version-information"></a>Informações sobre plataforma e versão  

 Saiba mais sobre suporte de versão e plataforma em [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  

  
## <a name="see-also"></a>Consulte Também

 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
