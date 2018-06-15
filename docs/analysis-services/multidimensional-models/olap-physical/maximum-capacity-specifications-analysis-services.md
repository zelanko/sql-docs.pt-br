---
title: Especificações de capacidade máxima (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 187a3a76f63853c63b9fe92dbd7ccfd4a0cfcdb5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027353"
---
# <a name="maximum-capacity-specifications-analysis-services"></a>Especificações de capacidade máxima (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  As tabelas a seguir especificam os tamanhos e números máximos de vários objetos definidos nos componentes do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] em diferentes modos de implantação de servidor.  
  
 Este tópico contém as seguintes seções:  
  
 [Multidimensional e mineração de dados (DeploymentMode = 0)](#bkmk_OLAP)  
  
 [SharePoint (DeploymentMode = 1)](#bkmk_sharepoint)  
  
 [Tabela (DeploymentMode = 2)](#bkmk_vertipaq)  
  
##  <a name="bkmk_OLAP"></a> Multidimensional e mineração de dados (DeploymentMode = 0)  
 O modo de armazenamento MOLAP que armazena dados e metadados tem limites físicos adicionais em tamanhos de arquivos. Os arquivos de repositório de cadeia de caracteres têm, por padrão, um tamanho máximo de 4 GB. Se você precisar de arquivos maiores para repositórios de cadeia de caracteres, poderá especificar outra arquitetura de armazenamento de cadeia de caracteres. Para obter mais informações, consulte [configurar o armazenamento de cadeia de caracteres para dimensões e partições](../../../analysis-services/multidimensional-models/configure-string-storage-for-dimensions-and-partitions.md).  
  
|Objeto|Tamanho máximo/números|  
|------------|----------------------------|  
|Bancos de dados em uma instância|2^31-1 = 2,147,483,647|  
|Dimensões em um banco de dados|2^31-1 = 2,147,483,647|  
|Atributos em uma dimensão|2^31-1 = 2,147,483,647|  
|Membros em um atributo de dimensão|2^31-1 = 2,147,483,647|  
|Hierarquias definidas pelo usuário em uma dimensão|2^31-1 = 2,147,483,647|  
|Níveis em uma hierarquia definida pelo usuário|2^31-1 = 2,147,483,647|  
|Cubos em um banco de dados|2^31-1 = 2,147,483,647|  
|Grupos de medida em um cubo|2^31-1 = 2,147,483,647|  
|Medidas em um grupo de medidas|2^31-1 = 2,147,483,647|  
|Cálculos em um cubo|2^31-1 = 2,147,483,647|  
|KPIs em um cubo|2^31-1 = 2,147,483,647|  
|Ações em um cubo|2^31-1 = 2,147,483,647|  
|Partições em um cubo|2^31-1 = 2,147,483,647|  
|Traduções em um cubo|2^31-1 = 2,147,483,647|  
|Agregações em uma partição|2^31-1 = 2,147,483,647|  
|Células retornadas por uma consulta|2^31-1 = 2,147,483,647|  
|Tamanho do registro da consulta de origem|64K|  
|Comprimento de nomes de objeto|100 caracteres|  
|Número máximo de estados distintos na coluna de atributos de modelo de mineração de dados|2^31-1 = 2,147,483,647|  
|Número máximo de atributos considerados (seleção de recursos)|2^31-1 = 2,147,483,647|  
  
 Para obter mais informações sobre as diretrizes de nomenclatura de objeto, consulte [objetos e características de objeto ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
 Para obter mais informações sobre limitações da fonte de dados para processamento analítico online (OLAP) e mineração de dados, consulte [suporte para fontes de dados &#40;SSAS - Multidimensional&#41;](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md), [ &#40;SSAS - Multidimensional&#41;](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md), e [objetos e características de objeto ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
##  <a name="bkmk_sharepoint"></a> SharePoint (DeploymentMode = 1)  
  
|Objeto|Tamanho máximo/números|  
|------------|----------------------------|  
|Bancos de dados em uma instância|2^31-1 = 2,147,483,647|  
|Tabelas em um banco de dados|2^31-1 = 2,147,483,647|  
|Colunas em uma tabela|2^31-1 = 2,147,483,647<br /><br /> **Aviso:** Número Total de colunas em uma tabela depende do número total de medidas e colunas calculadas associadas à mesma tabela.<br /><br /> O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Linhas em uma tabela|Ilimitado<br /><br /> **Aviso:** com a restrição que nenhum única coluna pode conter mais de 1.999.999.997 valores distintos.|  
|Hierarquias em uma tabela|2^31-1 = 2,147,483,647|  
|Níveis em uma hierarquia|2^31-1 = 2,147,483,647|  
|Relações|2^31-1 = 2,147,483,647|  
|Colunas de chave em uma tabela|2^31-1 = 2,147,483,647|  
|Medidas em uma tabela|2^31-1 = 2,147,483,647<br /><br /> **Aviso:** o número Total de medidas em uma tabela depende do número total de colunas e colunas calculadas associadas à mesma tabela.<br /><br /> O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Colunas calculadas em uma tabela|2^31-1 = 2,147,483,647<br /><br /> **Aviso:** o número Total de colunas calculadas em uma tabela depende do número total de colunas e medidas associados à mesma tabela.<br /><br /> O número máximo de 'Colunas + Medidas + Colunas Calculadas' para uma tabela é 2^31-1 = 2.147.483.647|  
|Células retornadas por uma consulta|2^31-1 = 2,147,483,647|  
|Tamanho do registro da consulta de origem|64K|  
|Comprimento de nomes de objeto|100 caracteres|  
  
##  <a name="bkmk_vertipaq"></a> Tabela (DeploymentMode = 2)  
Estes são os limites teóricos. Desempenho irá diminuir em números menores.   

|Objeto|Tamanho máximo/números|  
|------------|----------------------------|  
|Bancos de dados em uma instância|16,000|  
|Número combinado de tabelas e colunas em um banco de dados|16,000|  
|Linhas em uma tabela|Ilimitado<br /><br /> **Aviso:** com a restrição de que nenhuma coluna única na tabela pode ter mais de 1.999.999.997 valores distintos.|  
|Hierarquias em uma tabela|15,999|  
|Níveis em uma hierarquia|15,999|  
|Relações|8,000|  
|Colunas de chave na tabela de todos os|15,999|  
|Medidas em uma tabela|2^31-1 = 2,147,483,647|  
|Células retornadas por uma consulta|2^31-1 = 2,147,483,647|  
|Tamanho do registro da consulta de origem|64K|  
|Comprimento de nomes de objeto|no máximo 512 caracteres|  
  
## <a name="see-also"></a>Consulte também  
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Propriedades gerais](../../../analysis-services/server-properties/general-properties.md)  
  
  
