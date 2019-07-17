---
title: Alterações de comportamento | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fc9f8dcc3782204c8bf1c9add1200e451edcf127
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103872"
---
# <a name="behavioral-changes"></a>Alterações comportamentais
Alterações de comportamento são essas alterações para o qual o *sintaxe* da interface permanece a mesma, mas o *semântica* foram alterados. Para que essas alterações, a funcionalidade usada no ODBC 2. *x* se comporta de forma diferente do que a mesma funcionalidade em ODBC 3. *x*.  
  
 Se um aplicativo exibe o ODBC 2. *x* comportamento ou o ODBC 3. *x* comportamento é determinado pelo atributo SQL_ATTR_ODBC_VERSION ambiente. Esse valor de 32 bits é definido como SQL_OV_ODBC2 exibem o ODBC 2. *x* comportamento e SQL_OV_ODBC3 exibem o ODBC 3. *x* comportamento.  
  
 O atributo de ambiente SQL_ATTR_ODBC_VERSION é definido por uma chamada para **SQLSetEnvAttr**. Depois que um aplicativo chama **SQLAllocHandle** para alocar um identificador de ambiente, ele deve chamar**SQLSetEnvAttr** imediatamente para definir o comportamento que ele exibe. (Como resultado, há um novo estado de ambiente para descrever o identificador de ambiente em um alocados, mas automáticas sem versão, estado.) Para obter mais informações, consulte [apêndice b: Tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Um aplicativo declara que comportamento ele exibe um com o atributo de ambiente SQL_ATTR_ODBC_VERSION, mas o atributo não tem efeito sobre a conexão do aplicativo com um ODBC 2. *x* ou o ODBC 3. *x* driver. ODBC 3. *x* aplicativo pode se conectar a qualquer um uma ODBC 2. *x* ou 3. *x* driver, independentemente da configuração do atributo ambiente.  
  
 ODBC 3. *x* aplicativos nunca devem chamar **SQLAllocEnv**. Como resultado, se o Gerenciador de Driver recebe uma chamada para **SQLAllocEnv**, ele reconhece o aplicativo como um ODBC 2. *x* aplicativo.  
  
 O atributo SQL_ATTR_ODBC_VERSION afeta três diferentes aspectos de um ODBC 3. *x* comportamento do driver:  
  
-   SQLSTATEs  
  
-   Tipos de dados para data, hora e carimbo de hora  
  
-   O *CatalogName* argumento **SQLTables** aceita padrões de pesquisa em ODBC 3. *x*, mas não no ODBC 2. *x*  
  
 Não afeta a configuração do atributo ambiente SQL_ATTR_ODBC_VERSION **SQLSetParam** ou **SQLBindParam**. **SQLColAttribute** também não é afetado por esse bit. Embora **SQLColAttribute** retorna atributos que são afetados pela versão do ODBC (tipo de data, precisão, escala e comprimento), o comportamento desejado é determinado pelo valor da *FieldIdentifier*argumento. Quando *FieldIdentifier* é igual a SQL_DESC_TYPE, **SQLColAttribute** retorna o ODBC 3. *x* códigos de data, hora e carimbo de hora; quando *FieldIdentifier* é igual a SQL_COLUMN_TYPE, **SQLColAttribute** retorna o ODBC 2. *x* códigos de data, hora e carimbo de hora.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Mapeamentos SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Alterações de tipo de dados datetime](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
