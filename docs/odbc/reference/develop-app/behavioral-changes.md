---
title: Mudanças comportamentais | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e4a433531d90eb0f89d9a5e446464b13fd02526
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283436"
---
# <a name="behavioral-changes"></a>Alterações comportamentais
Mudanças comportamentais são aquelas mudanças para as quais a *sintaxe* da interface permanece a mesma, mas a *semântica* mudou. Para essas alterações, funcionalidade utilizada no ODBC 2. *x* se comporta de forma diferente da mesma funcionalidade no ODBC 3. *x*.  
  
 Se um aplicativo exibe ODBC 2. *x* comportamento ou ODBC 3. *x* o comportamento é determinado pelo SQL_ATTR_ODBC_VERSION atributo do ambiente. Este valor de 32 bits está definido para SQL_OV_ODBC2 para exibir ODBC 2. *x* comportamento, e SQL_OV_ODBC3 para exibir ODBC 3. *x* comportamento.  
  
 O SQL_ATTR_ODBC_VERSION atributo ambiente é definido por uma chamada para **SQLSetEnvAttr**. Depois que um aplicativo chama **o SQLAllocHandle** para alocar uma alça de ambiente, ele deve chamar**o SQLSetEnvAttr** imediatamente para definir o comportamento que exibe. (Como resultado, há um novo estado ambiental para descrever a alça do ambiente em um estado alocado, mas sem versão.) Para obter mais informações, consulte [o apêndice B: Tabelas de transição do estado oDBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Um aplicativo afirma qual comportamento ele exibe com o atributo ambiente SQL_ATTR_ODBC_VERSION, mas o atributo não tem efeito na conexão do aplicativo com um ODBC 2. *x* ou ODBC 3. *x* driver. Um ODBC 3. *x* aplicativo pode se conectar a um ODBC 2. *x* ou 3. *x* driver, não importa qual a configuração do atributo do ambiente.  
  
 ODBC 3. *x* aplicativos nunca devem chamar **SQLAllocEnv**. Como resultado, se o Driver Manager receber uma chamada para **SQLAllocEnv,** ele reconhecerá o aplicativo como um ODBC 2. *x* aplicação.  
  
 O atributo SQL_ATTR_ODBC_VERSION afeta três aspectos diferentes de um ODBC 3. *x* comportamento do driver:  
  
-   SQLSTATEs  
  
-   Tipos de dados para data, hora e carimbo de data  
  
-   O argumento *CatalogName* no **SQLTables** aceita padrões de pesquisa no ODBC 3. *x*, mas não em ODBC 2. *x*  
  
 A configuração do SQL_ATTR_ODBC_VERSION atributo do ambiente não afeta **SQLSetParam** ou **SQLBindParam**. **SQLColAttribute** também não é afetado por essa parte. Embora **o SQLColAttribute devolva** atributos que são afetados pela versão do ODBC (tipo de data, precisão, escala e comprimento), o comportamento pretendido é determinado pelo valor do argumento *FieldIdentifier.* Quando *fieldidentifier* é igual a SQL_DESC_TYPE, **SQLColAttribute** retorna o ODBC 3. *x* códigos para data, hora e carimbo de data; quando *fieldidentifier* é igual a SQL_COLUMN_TYPE, **SQLColAttribute** retorna o ODBC 2. *x* códigos para data, hora e carimbo de data.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Mapeamentos de SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Alterações de tipo de dados datetime](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
