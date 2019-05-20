---
title: Destino do Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSDEST.F1
- sql14.dts.designer.afpadlsdest.f1
ms.assetid: 4c4f504f-dd2b-42c5-8a20-1a8ad9a5d632
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: da23e2b0bdda3c99babe18d500edace9d18f9ca4
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727202"
---
# <a name="azure-data-lake-store-destination"></a>Destino do Azure Data Lake Store

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O componente **Destino do Azure Data Lake Store** permite que um pacote SSIS grave dados em um Azure Data Lake Store. Os formatos de arquivo compatíveis são: Texto, Avro e ORC. 
  
 O **Destino do Azure Data Lake Store** é um componente do [SSIS (SQL Server Integration Services) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
 
> [!NOTE]
> Para garantir que o Gerenciador de conexões do Azure Data Lake Store e os componentes que o utilizam, isto é, a Fonte do Azure Data Lake Store e o Destino do Azure Data Lake Store, possam se conectar aos serviços, verifique se você baixou a versão mais recente do Azure Feature Pack [aqui](https://www.microsoft.com/download/details.aspx?id=49492). 

## <a name="configure-the-azure-data-lake-store-destination"></a>Configure o Destino do Azure Data Lake Store  
1. Arraste e solte **Destino do Azure Data Lake Store** para o designer de fluxo de dados e clique duas vezes nele para ver o editor.  

2.  Para o campo **Gerenciador de conexões do Azure Data Lake Store** , especifique um Gerenciador de conexões do Azure Data Lake Store existente ou crie um novo referindo-se a um serviço do Azure Data Lake Store.  
  
    1.  Para o **caminho do arquivo** especifique o nome do arquivo em que você deseja gravar dados. Se esse arquivo já existir, o conteúdo será substituído.  
  
    2.  Para o campo **Formato de arquivo** , especifique o formato de arquivo que você deseja usar.  
  
       Se o formato de arquivo for texto, você deverá especificar o valor do **Caractere delimitador de coluna** . Além disso, escolha **Nomes de coluna na primeira linha de dados** se a primeira linha no arquivo contiver nomes de coluna.  

       Se o formato do arquivo for ORC, será preciso instalar o Java Runtime Environment (JRE) para a plataforma apropriada.
  
3.  Depois de especificar as informações de conexão, alterne para a página **Colunas** para mapear colunas de origem para colunas de destino para o fluxo de dados do SSIS.  
