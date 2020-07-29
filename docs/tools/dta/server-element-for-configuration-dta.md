---
title: Elemento de servidor para configuração (DTA)
description: No utilitário dta, o elemento Server de Configuration contém as informações de identificação do servidor no qual você deseja avaliar uma configuração.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: dd7c6d0c32ab3e5cdffaf66765ca05b8995ef440
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732059"
---
# <a name="server-element-for-configuration-dta"></a>Elemento de servidor para configuração (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Contém as informações de identificação para o servidor no qual você quer que o Orientador de Otimização do Mecanismo de Banco de Dados avalie uma configuração hipotética (especificada pelo elemento de **Configuração** ).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Obrigatório uma vez por elemento de **Configuração** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Configuration &#40;DTA&#41;](../../tools/dta/configuration-element-dta.md)|  
|**Elementos filho**|[Elemento Name para Server &#40;DTA&#41;](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [Elemento Database para Configuration &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>Comentários  
 Você pode especificar apenas um elemento de **servidor** para o elemento de **configuração** . Esse elemento tem o nome **ServerTypecomplexType** no [Esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?linkid=43100). Não confunda esse elemento de **servidor** com aquele que é o filho do elemento **DTAInput** . Para obter mais informações, consulte [Elemento de servidor &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso, consulte a [Amostra de arquivo de entrada XML com a configuração especificada pelo usuário &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
