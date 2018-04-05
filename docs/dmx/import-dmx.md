---
title: IMPORTAÇÃO (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IMPORT
dev_langs:
- DMX
helpviewer_keywords:
- IMPORT statement
- mining structures [DMX], importing
ms.assetid: c053bc88-2daf-4ebb-81d7-5a330250536d
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1cf52d8c9e9430fcc1059cc3df2e01cf5ed03ce8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Carrega um modelo de mineração ou estrutura de mineração de um arquivo .abf (Analysis Services Backup) no servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome de arquivo*  
 Uma cadeia de caracteres que contém o nome e o local do arquivo a ser importado.  
  
## <a name="remarks"></a>Remarks  
 Se nenhum objeto for especificado, serão carregados os conteúdos inteiros do arquivo .dmb. Se o arquivo .dmb incluir um banco de dados não existente no servidor, o banco de dados será criado.  
  
 É preciso ser um banco de dados ou administrador de servidor para exportar ou importar objetos.  
  
## <a name="import-from-file-example"></a>Exemplo de importar do arquivo  
 O exemplo a seguir importa todo o conteúdo do arquivo com o modelo e a estrutura de associação para o servidor atual.  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões de mineração de dados &#40; DMX &#41; Instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [EXPORTAR &#40; DMX &#41;](../dmx/export-dmx.md)   
 [Exportar e importar objetos de Mineração de dados](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
