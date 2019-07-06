---
title: Fontes de dados com suporte em modelos do SQL Server Analysis Services tabulares 1200 | Microsoft Docs
ms.date: 07/02/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1ef7ae48e3d1500d08c9adba5e39db6214125c5
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597358"
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1200-models"></a>Fontes de dados com suporte no SQL Server Analysis Services, modelos de tabela 1200
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  
Este artigo descreve os tipos de fontes de dados que podem ser usados com modelos de tabela do SQL Server Analysis Services no 1200 e nível de compatibilidade inferior. 

Para modelos nos níveis de compatibilidade 1400, consulte [fontes de dados com suporte nos modelos do SQL Server Analysis Services tabular 1400](data-sources-supported-ssas-tabular-1400.md).

Para o Azure Analysis Services, consulte [fontes de dados com suporte no Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource).
  
##  <a name="bkmk_supported_ds"></a> Fontes de dados com suporte para modelos de tabela na memória  
Quando você instalar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a instalação não instala os provedores listados para cada fonte de dados. Alguns provedores podem ser instalados com outros aplicativos em seu computador. Em outros casos, você precisa baixar e instalar o provedor.  
  
|||||  
|-|-|-|-|  
|`Source`|Versões|Tipo de arquivo|Provedores|  
|Bancos de dados do Access|Microsoft Access 2010 e posterior.|.accdb ou .mdb|Provedor OLE DB ACE 14 <sup> [1](#dnu)</sup>|  
|Bancos de dados relacionais do SQL Server|SQL Server 2008 e posterior, o depósito de dados do SQL Server 2008 e posterior, o Azure banco de dados SQL do Azure SQL Data Warehouse, Analytics Platform System (APS)<br /><br /> <br /><br /> Analytics Platform System (APS) era anteriormente conhecido como SQL Server Parallel Data Warehouse (PDW). Originalmente, conectar o PDW a partir do Analysis Services exigia um provedor de dados especial. Esse provedor foi substituído no SQL Server 2012. A partir do SQL Server 2012, o cliente nativo do SQL Server é usado para as conexões com o PDW/APS. |(não se aplica)|Provedor OLE DB para SQL Server<br /><br /> Provedor OLE DB do SQL Server Native Client<br /><br /> Provedor OLE DB do SQL Server Native 10.0 Client<br /><br /> Provedor de dados .NET Framework para SQL Client|  
|Bancos de dados relacionais da Oracle|Oracle 9i e posterior.|(não se aplica)|Provedor OLE DB Oracle<br /><br /> Provedor de Dados .NET Framework para Cliente Oracle<br /><br /> Provedor de dados do .NET Framework para SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Bancos de dados relacionais do Teradata|Teradata V2R6 e posterior|(não se aplica)|Provedor OLE DB TDOLEDB<br /><br /> Provedor de .NET Data para Teradata|  
|Bancos de dados relacionais do Informix||(não se aplica)|Provedor OLE DB para Informix|  
|Bancos de dados relacionais IBM DB2|8.1|(não se aplica)|DB2OLEDB|  
|Bancos de dados relacionais do Sybase Adaptive Server Enterprise (ASE)|15.0.2|(não se aplica)|Provedor OLE DB para Sybase|  
|Outros bancos de dados relacionais|(não se aplica)|(não se aplica)|Provedor OLE DB para driver ODBC|  
|Arquivos de texto|(não se aplica)|.txt, .tab, .csv|Provedor OLE DB ACE 14 <sup> [1](#dnu)</sup> |  
|Arquivos do Microsoft Excel|Excel 2010 e posterior|.xlsx, xlsm, .xlsb, .xltx, .xltm|Provedor OLE DB ACE 14 <sup> [1](#dnu)</sup>|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pasta de trabalho|Microsoft SQL Server 2008 Analysis Services e posterior|xlsx, xlsm, .xlsb, .xltx, .xltm|ASOLEDB 10.5<br /><br /> (usado apenas com pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] publicadas em farms do SharePoint com o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] instalado)|  
|Cubo do Analysis Services|Microsoft SQL Server 2008 Analysis Services e posterior|(não se aplica)|ASOLEDB 10|  
|Alimentações de dados<br /><br /> (usado para importar dados de relatórios do Reporting Services, documentos do serviço Atom, Microsoft Azure Marketplace DataMarket e feed de dados único)|Formato Atom 1.0<br /><br /> Qualquer banco de dados ou documento exposto como um Serviço de dados do WCF (Windows Communication Foundation) (antes ADO.NET Data Services).|`.atomsvc` para um documento de serviço que define um ou mais feeds<br /><br /> .atom para um documento de feed da Web do Atom|Provedor de Feed de Dados Microsoft para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> Provedor de dados do feed de dados do .NET Framework para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Arquivos de conexão de banco de dados do Office||.odc||  
 
<a name="dnu">[1] </a> Using **ACE 14 OLE DB provider** para conectar-se aos tipos de dados de arquivo **não é recomendável**. Se for preciso manter seus modelos de nível de compatibilidade 1200 e inferior, exporte os dados para um tipo de arquivo csv, importar banco de dados SQL e, em seguida, conectar e importar do banco de dados. No entanto, recomenda-se você atualizar para o nível de compatibilidade 1400 (SQL Server 2017 e posterior) e usar **obter dados** no SSDT para selecionar e importar sua fonte de dados de arquivo. Obter usos dados estruturados conexões fonte de dados fornecidas pelo mecanismo de dados do Power Query, que são mais estáveis que as conexões de provedor de ACE 14 OLE DB.  


##  <a name="bkmk_supported_ds_dq"></a> Fontes de dados com suporte para modelos DirectQuery  
 O DirectQuery é uma alternativa para o modo de armazenamento na memória, roteando consultas e retornando os resultados diretamente em sistemas de dados de back-end em vez de armazenar todos os dados dentro do modelo (e na RAM depois que o modelo é carregado). Porque o Analysis Services tem que formular consultas na sintaxe de consulta de banco de dados nativo, um subconjunto menor de fontes de dados tem suporte para esse modo.  
  
Fonte de dados   |Versões  |Provedores
---------|---------|---------
Microsoft SQL Server    |  2008 e posterior      |       Provedor OLE DB para SQL Server, Provedor OLE DB para SQL Server Native Client, Provedor de Dados .NET Framework para SQL Client  
Banco de Dados SQL do Microsoft Azure    |   Todos      |  Provedor OLE DB para SQL Server, Provedor OLE DB para SQL Server Native Client, Provedor de Dados .NET Framework para SQL Client            
SQL Data Warehouse do Microsoft Azure     |   Todos     |  Provedor OLE DB para SQL Server Native Client, Provedor de Dados .NET Framework para SQL Client       
Microsoft SQL APS (Analytics Platform System)     |   Todos      |  Provedor OLE DB para SQL Server, Provedor OLE DB para SQL Server Native Client, Provedor de Dados .NET Framework para SQL Client       
|Microsoft SQL Server Always Encrypted <sup> [2](#ae)</sup> | 2016 e posterior. 2014 e anterior apenas a Enterprise edition. | Provedor de dados .NET Framework para SQL Client
|Banco de dados SQL do Azure Always Encrypted <sup> [2](#ae)</sup>| Todos | Provedor de dados .NET Framework para SQL Client
Bancos de dados relacionais da Oracle     |  Oracle 9i e posterior       |  Provedor OLE DB Oracle       
Bancos de dados relacionais do Teradata    |  Teradata V2R6 e posterior     | Provedor de .NET Data para Teradata    


### <a name="using-sql-server-analysis-services-with-always-encrypted"></a>Usando o SQL Server Analysis Services com o Always Encrypted

<a name="ae">[2] </a> SQL Server Analysis Services pode agir como um cliente para um banco de dados usando [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) no SQL Server ou banco de dados SQL Azure nas seguintes condições: 

*  Chaves mestras de coluna protegendo as colunas criptografadas devem ser certificados, armazenados no repositório de certificados do Windows. Não há suporte para chaves mestras de coluna armazenadas no cofre de chaves do Azure.   
*  O computador do Windows em que o Analysis Services está instalado tem os certificados de chave mestra de coluna necessários instalados. Para obter mais informações, consulte [Criando chaves mestras de coluna na Windows Store de certificado](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-windows-certificate-store).
*  A fonte de dados do Analysis Services usa para se conectar ao SQL se baseia no .net Framework provider e a configuração de criptografia de coluna de propriedade na fonte de dados deve ser habilitada. .NET framework 4.6.1 ou posterior deve estar presente no servidor do Analysis Services.
*  A fonte de dados do SQL Server ou banco de dados SQL deve ser um *provedor* tipo de fonte de dados com suporte de nível de compatibilidade 1200. Ele não funcionará com o Power Query *estruturados* fontes de dados, introduzidos no nível de compatibilidade 1400.
  
##  <a name="bkmk_tips"></a> Dicas para escolher fontes de dados  
  
A importação de tabelas de bancos de dados relacionais elimina etapas pois são usadas relações de *chave estrangeira* durante a importação para criar relações entre as tabelas no designer de modelos.  
  
Você também pode eliminar etapas com a importação de várias tabelas e a exclusão das tabelas desnecessárias. Se você importar uma tabela de cada vez, talvez ainda precise criar relações manualmente entre tabelas.  
  
Colunas que contêm dados semelhantes em fontes de dados diferentes são a base para criar relações dentro do designer de modelos. Ao usar fontes de dados heterogêneos, escolha tabelas com colunas que possam ser mapeadas para tabelas em outras fontes de dados que contêm dados idênticos ou semelhantes.  
  
Provedores OLE DB, às vezes, podem oferecer um desempenho mais rápido para dados em larga escala. Ao escolher entre diferentes provedores para a mesma fonte de dados, experimente primeiro o provedor OLE DB.  

## <a name="see-also"></a>Confira também

[Fontes de dados com suporte no SQL Server Analysis Services, modelos de tabela 1400](data-sources-supported-ssas-tabular-1400.md)

[Fontes de dados com suporte no Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
