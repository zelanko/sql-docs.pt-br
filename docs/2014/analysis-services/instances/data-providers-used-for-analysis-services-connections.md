---
title: Provedores de dados usados para conexões de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 128f6dde-409d-4c12-9820-3305bab57b75
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 16e691ab6c6a6fcff4cb59fe54884fbb1b52268e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080096"
---
# <a name="data-providers-used-for-analysis-services-connections"></a>Provedores de dados usados para conexões do Analysis Services
  O Analysis Services fornece três provedores de dados do servidor e acesso a dados. Todos os aplicativos que se conectam ao Analysis Services fazem isso usando um desses provedores. Dois dos provedores, ADOMD.NET e AMO (objetos de gerenciamento do Analysis Services), são provedores de dados gerenciados. O provedor OLE DB do Analysis Services (MSOLAP DLL) é um provedor de dados nativo.  
  
 Em organizações que executam muitas versões do Analysis Services, talvez seja necessário instalar versões mais recentes dos provedores de dados nas estações de trabalho de usuário que se conectam a dados do Analysis Services. As conexões a novas versões do Analysis Services exigem que os provedores de dados estejam na mesma versão principal. Por exemplo, para se conectar ao [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)], cada estação de trabalho deve ter um provedor de dados da versão 2014. Embora o Excel instale os provedores de dados ao quais você precisa se conectar, esse provedor pode estar desatualizado em relação às instâncias do Analysis Services que você está usando.  
  
 Este tópico inclui as seções a seguir:  
  
 [Como determinar a versão do servidor](#bkmk_ServVers)  
  
 [Como determinar a versão dos provedores de dados do Analysis Services](#bkmk_LibUpdate)  
  
 [Onde obter as versões mais recentes dos provedores de dados](#bkmk_downloadsite)  
  
 [Provedor OLE DB para Analysis Services](#bkmk_OLE)  
  
 [ADOMD.NET](#bkmk_ADOMD)  
  
 [AMO](#blkmk_AMO)  
  
##  <a name="how-to-determine-server-version"></a><a name="bkmk_ServVers"></a>Como determinar a versão do servidor  
 Conhecer a versão da instância do Analysis Services o ajudará a determinar se você precisa instalar versões mais recentes dos provedores de dados nas estações de trabalho da sua organização.  
  
-   No SQL Server Management Studio, conecte-se à instância do Analysis Services. Clique com o botão direito do mouse na instância que você deseja verificar, aponte para **relatórios**e clique em **geral**. As informações sobre a versão e a edição serão exibidas no relatório.  
  
 O número principal da versão inicial do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] é 12.0.2000.9.  
  
 Para obter mais informações sobre como descobrir a versão e a edição do SQL Server, consulte [Como determinar a versão e a edição do SQL Server e seus componentes](https://support.microsoft.com/kb/321185).  
  
##  <a name="how-to-determine-the-version-of-the-analysis-services-data-providers"></a><a name="bkmk_LibUpdate"></a>Como determinar a versão do Analysis Services provedores de dados  
 Os provedores de dados são instalados com o Analysis Services, bem como por aplicativos cliente que se conectam rotineiramente a bancos de dados do Analysis Services, como o Excel.  
  
 O Office 2007 instala provedores de dados do SQL Server 2005. O Office 2010 instala provedores de dados do SQL Server 2008. O Office 2013 instala provedores de dados do SQL Server 2012. Se você estiver usando várias versões do Office ou do SQL Server, e as conexões ou a disponibilidade de recursos não forem as que você esperava, talvez seja necessário instalar uma versão mais recente dos provedores de dados. Você pode executar diversas versões principais de cada provedor de dados lado a lado no mesmo computador.  
  
#### <a name="find-the-file-version-of-the-oledb-provider"></a>Localizar a versão do arquivo do provedor OLE DB  
  
1.  Vá para \Arquivos de Programas\Microsoft Analysis Services\AS OLEDB\120.  
  
2.  Clique com o botão direito do mouse em msolap120. dll e clique em **Propriedades**.  
  
 Se você não conseguir localizar o arquivo nesse local, ou se o caminho da pasta incluir AS OLEDB\110 ou AS OLEDB\90, você está usando uma biblioteca antiga e deve instalar a versão mais recente agora (AS OLEDB\11) para conectar-se ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
#### <a name="find-the-file-version-of-adomdnet-and-amo"></a>Localizar a versão dos arquivos do ADOMD.NET e do AMO  
  
1.  Vá para C:\Windows\Assembly  
  
2.  Clique com o botão direito do mouse em Microsoft.AnalysisServices.AdomdClient e clique em **Propriedades**. Clique em **Versão**.  
  
     Para descobrir a versão do arquivo do AMO, clique com o botão direito do mouse em Microsoft.AnalysisServices.  
  
 Para obter mais informações sobre os números de versão por lançamento, consulte [Builds do SQL Server no Blogspot](http://sqlserverbuilds.blogspot.com).  
  
##  <a name="where-to-get-newer-version-data-providers"></a><a name="bkmk_downloadsite"></a>Onde obter provedores de dados de versão mais recentes  
 A versão instalada no computador cliente deve corresponder à versão principal do servidor que fornece os dados. Se a instalação do servidor for mais recente do que a instalação dos provedores de dados existentes nas estações de trabalho da sua rede, talvez você precise instalar bibliotecas mais recentes.  
  
#### <a name="find-the-data-providers-on-the-download-site"></a>Localizar os provedores de dados no site de download  
  
1.  Vá para o [centro de download da Microsoft](https://go.microsoft.com/fwlink/p/?LinkID=296473).  
  
2.  Expanda a seção **Instruções de instalação**.  
  
3.  Role a tela para baixo até a seção que contém os componentes do Analysis Services. ADOMD.NET, o provedor OLE DB, e AMO são respectivamente a segunda, terceira e quarta opções na lista. Cada biblioteca está disponível em versões de 32 bits e de 64 bits. Os servidores e estações de trabalho mais recentes que estejam executando um sistema operacional de 64 bits necessitarão da versão de 64 bits.  
  
##  <a name="analysis-services-ole-db-provider"></a><a name="bkmk_OLE"></a>Provedor Analysis Services OLE DB  
 O Provedor OLE DB para Analysis Services é o provedor nativo das conexões de banco de dados do Analysis Services. O MSOLAP é usado indiretamente pelo ADOMD.NET e pelo AMO, delegando solicitações de conexão ao provedor de dados. Você também pode chamar o provedor OLE DB diretamente do código do aplicativo, o que você poderá fazer se os requisitos de solução impedirem o uso da API gerenciada.  
  
 O provedor OLE DB para Analysis Services é instalado automaticamente pela Instalação do SQL Server, pelo Excel e por outros aplicativos que costumam ser usados para acessar bancos de dados do Analysis Services. Você também pode instalá-lo manualmente, baixando-o do Centro de download da Microsoft. Por padrão, o provedor pode ser encontrado na pasta \Arquivos de Programas\Microsoft Analysis Services. O provedor deve ser instalado em qualquer estação de trabalho usada para acessar dados do Analysis Services.  
  
 MSOLAP130.dll é a versão do provedor OLE DB para Analysis Services fornecida com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Outras versões anteriores recentes incluem o MSOLAP10.dll (para SQL Server 2008 e 2008 R2) e o MSOLAP90.dll (para SQL Server 2005).  
  
 Provedores de OLE DB costumam ser especificados em cadeias de conexão. Uma cadeia de conexão Analysis Services usa um nomenclatura diferente para fazer referência ao provedor de OLE DB: MSOLAP. \<versão>. dll  
  
 O MSOLAP.5.dll é o provedor OLE DB atual do Analysis Services instalado com o Excel 2013. As versões anteriores, como MSOLAP.4.dll ou MSOLAP.3.dll, geralmente são encontradas em estações de trabalho que executam versões anteriores do Excel. Alguns recursos do Analysis Services, como o suplemento PowerPivot, exigem versões específicas do provedor OLE DB. Consulte [Propriedades da cadeia de conexão &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md) para obter mais informações.  
  
##  <a name="adomdnet"></a><a name="bkmk_ADOMD"></a>ADOMD.NET  
 O ADOMD.NET é um provedor de dados gerenciado usado para consultar dados do Analysis Services. O Excel usa o ADOMD.NET ao se conectar a um cubo específico do Analysis Services. A cadeia de conexão que você vê no Excel destina-se a uma conexão do ADOMD.NET.  
  
 O ADOMD.NET é instalado pela Instalação do SQL Server e usado por aplicativos cliente do SQL Server para conectar-se ao Analysis Services. O Office instala esta biblioteca para dar suporte a conexões de dados do Excel. Assim como em outros provedores de dados incluídos no SQL Server, você poderá redistribuir o ADOMD.NET se estiver usando a biblioteca em código personalizado. Você também pode baixar e instalá-lo manualmente para obter a versão mais recente (consulte [Como determinar a versão dos provedores de dados do Analysis Services](#bkmk_LibUpdate) neste tópico).  
  
 Para verificar informações da versão do arquivo, procure ADOMD.NET no cache de assembly global, onde ele é listado como `Microsoft.AnalysisServices.AdomdClient`.  
  
 Ao conectar-se a um banco de dados, as propriedades da cadeia de conexão das três bibliotecas são basicamente as mesmas. Quase todas as cadeias de conexão que você define para o ADOMD.NET (<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>) também funcionarão para o AMO e o provedor OLE DB para Analysis Services. Consulte [Propriedades da cadeia de conexão &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md) para obter mais informações.  
  
 Para obter mais informações sobre conexões programáticas, consulte [Establishing Connections in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net).  
  
##  <a name="amo"></a><a name="blkmk_AMO"></a>AMO  
 O AMO é um provedor de dados gerenciado usado para administração do servidor e definição de dados. Por exemplo, o SQL Server Management Studio usa o AMO para se conectar ao Analysis Services.  
  
 O AMO é instalado pela Instalação do SQL Server e usado por aplicativos cliente do SQL Server para conectar-se ao Analysis Services. Você também pode baixar e instalá-lo manualmente usando o AMO em código personalizado (consulte [Como determinar a versão dos provedores de dados do Analysis Services](#bkmk_LibUpdate) neste tópico). O AMO pode ser encontrado no cache de assembly global, como `Microsoft.AnalysisServices`.  
  
 Uma conexão usando AMO normalmente é mínima, consistindo em "Data Source =\<servername>". Depois que uma conexão é estabelecida, você usa a API para trabalhar com coleções de banco de dados e grandes objetos. Tanto o SSDT quanto o SSMS usam o AMO para se conectar a uma instância do Analysis Services.  
  
 Para obter mais informações sobre conexões programáticas, consulte [Programming AMO Fundamental Objects](https://docs.microsoft.com/bi-reference/amo/programming-amo-fundamental-objects).  
  
## <a name="see-also"></a>Consulte Também  
 [Conectar ao Analysis Services](connect-to-analysis-services.md)  
  
  
