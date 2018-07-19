---
title: IMPORTAÇÃO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4987701deb466148253c8418c88683d2dbfbc16b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38061020"
---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Carrega um modelo de mineração ou estrutura de mineração de um arquivo .abf (Analysis Services Backup) no servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>Argumentos  
 *filename*  
 Uma cadeia de caracteres que contém o nome e o local do arquivo a ser importado.  
  
## <a name="remarks"></a>Remarks  
 Se nenhum objeto for especificado, serão carregados os conteúdos inteiros do arquivo .dmb. Se o arquivo .dmb incluir um banco de dados não existente no servidor, o banco de dados será criado.  
  
 É preciso ser um banco de dados ou administrador de servidor para exportar ou importar objetos.  
  
## <a name="import-from-file-example"></a>Exemplo de importar do arquivo  
 O exemplo a seguir importa todo o conteúdo do arquivo com o modelo e a estrutura de associação para o servidor atual.  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [EXPORTAR &AMP;#40;DMX&AMP;#41;](../dmx/export-dmx.md)   
 [Exportar e importar objetos de Mineração de dados](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
