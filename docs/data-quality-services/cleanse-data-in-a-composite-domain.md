---
title: "Limpar dados em um domínio de composição | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7d1076e0-7710-469a-9107-e293e4bd80ac
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2097ea11b3ab85e39ec6be4c62d0526aac9f61d5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="cleanse-data-in-a-composite-domain"></a>Limpar dados em um domínio composto
  Este tópico fornece informações sobre como limpar domínios compostos no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Um domínio composto consiste em dois ou mais domínios únicos, e é mapeado para um campo de dados que consiste em vários termos relacionados. Os domínios individuais em um domínio composto devem ter uma área comum de conhecimento. Para obter informações detalhadas sobre domínios compostos, consulte [Managing a Composite Domain](../data-quality-services/managing-a-composite-domain.md).  
  
##  <a name="Mapping"></a> Mapeando um domínio composto para os dados de origem  
 Há dois modos para mapear seus dados de origem para um domínio composto:  
  
-   Os dados de origem são um único campo (digamos Nome Completo), que é mapeado para um domínio composto.  
  
    -   Se o domínio composto for mapeado para um serviço de dados de referência, os dados de origem serão enviados como tal para o serviço de dados de referência para correção e análise.  
  
    -   Se o domínio composto não for mapeado para um serviço de dados de referência, a análise se baseará no método de análise definido no domínio composto. Para obter mais informações sobre como especificar um método de análise para domínios compostos, consulte [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md)  
  
-   Os dados de origem consistem em vários campos (digamos First Name, Middle Name e Last Name) que são mapeados para domínios individuais em um domínio composto.  
  
 Para obter um exemplo de como mapear domínios de composição para dados de origem, consulte [Anexar um domínio ou um domínio de composição aos dados de referência](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
##  <a name="CDCorrection"></a> Correção de dados usando regras de domínio cruzado definitivas  
 As regras do domínio cruzado no domínio composto permitem que você crie regras que indicam a relação entre domínios individuais em um domínio composto. As regras do domínio cruzado são levadas em conta quando você executa a atividade de limpeza em seus dados de origem envolvendo domínios compostos. Além de informá-lo sobre a validade de uma regra de domínio cruzado, a regra de domínio cruzado *Then* , **Valor é igual a**, também corrige os dados durante a atividade de limpeza de dados.  
  
 Considere o seguinte exemplo: há um domínio composto, Product, com três domínios individuais: ProductName, CompanyName e ProductVersion. Crie a seguinte regra de domínio cruzado definitiva:  
  
 O valor de domínio IF 'CompanyName' contém *Microsoft* e o valor de domínio 'ProductName' equivale a *Office* ; o valor 'ProductVersion' equivale a *2010* . O valor de domínio THEN 'ProductName' Valor equivale a *Microsoft Office 2010*.  
  
 Quando esta regra de domínio cruzado é executada, os dados de origem (ProductName) são corrigidos da seguinte forma após a atividade de limpeza:  
  
 **Dados de origem**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Office|Microsoft Inc.|2010|  
  
 **Dados de saída**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Microsoft Office 2010|Microsoft Inc.|2010|  
  
 Quando você testa a regra de domínio cruzado *Then* definitiva, **Valor é igual a**, a caixa de diálogo **Testar Regra de Domínio Composto** contém uma nova coluna, **Corrigir para**, que exibe os dados corretos. Em um projeto de qualidade de dados de limpeza, essa regra de domínio cruzado definitiva altera os dados com 100% de confiança e a coluna **Motivo** exibe a seguinte mensagem: Corrigido pela regra “*\<Cross-Domain Rule Name>*”. Para obter mais informações sobre regras de domínio cruzado, consulte [Create a Cross-Domain Rule](../data-quality-services/create-a-cross-domain-rule.md).  
  
> [!NOTE]  
>  A regra do domínio cruzado definitiva não funcionará para domínios compostos que estão anexados ao serviço de dados de referência.  
  
##  <a name="DataProfiling"></a> Criação de perfis de dados para domínios compostos  
 A criação de perfil do DQS fornece duas dimensões de qualidade de dados: *integridade* (até que ponto os dados estão presentes) e *exatidão* (até que ponto os dados podem ser empregados para o uso pretendido) durante a atividade de limpeza. A criação de perfil talvez não forneça estatísticas confiáveis de integridade para domínios compostos. Se você precisar de estatísticas de integridade, use domínios únicos, em vez de domínios compostos. Para utilizar domínios compostos, talvez você queira criar uma base de dados de conhecimento com domínios únicos para a criação de perfil, a fim de determinar a integridade e criar outro domínio com um domínio composto para a atividade de limpeza. Por exemplo, a criação de perfil pode mostrar 95% de integridade para registros de endereço usando um domínio composto, mas pode haver um nível muito mais alto de não integridade para uma das colunas, por exemplo, uma coluna de CEP. Neste exemplo, talvez você queira medir a integridade da coluna de CEP com um domínio único.  
  
 A criação de perfil provavelmente fornecerá estatísticas de exatidão confiáveis para domínios compostos, pois é possível medir a exatidão para várias colunas juntas. O valor desses dados está na agregação composta, de modo que talvez você queira medir a exatidão com um domínio composto.  
  
 Para obter informações detalhadas sobre a criação de perfil de dados durante a atividade de limpeza, consulte [Estatísticas do criador de perfil](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Profiler) em [Limpar dados usando o conhecimento &#40;interno&#41; do DQS](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
  
