---
title: Alterações comportamentais | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103872"
---
# <a name="behavioral-changes"></a>Alterações comportamentais
Alterações comportamentais são aquelas alterações para as quais a *sintaxe* da interface permanece a mesma, mas a *semântica* mudou. Para essas alterações, a funcionalidade usada no ODBC 2. *x* se comporta de forma diferente da mesma funcionalidade no ODBC 3. *x*.  
  
 Se um aplicativo exibe ODBC 2. comportamento *x* ou ODBC 3. o comportamento *x* é determinado pelo atributo de ambiente SQL_ATTR_ODBC_VERSION. Esse valor de 32 bits é definido como SQL_OV_ODBC2 para exibir ODBC 2. comportamento *x* e SQL_OV_ODBC3 para exibir o ODBC 3. comportamento *x* .  
  
 O atributo de ambiente SQL_ATTR_ODBC_VERSION é definido por uma chamada para **SQLSetEnvAttr**. Depois que um aplicativo chama **SQLAllocHandle** para alocar um identificador de ambiente, ele deve chamar**SQLSetEnvAttr** imediatamente para definir o comportamento que ele exibe. (Como resultado, há um novo estado de ambiente para descrever o identificador de ambiente em um estado alocado, mas sem versão). Para obter mais informações, consulte o [Apêndice B: tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Um aplicativo informa o comportamento que ele exibe com o atributo de ambiente SQL_ATTR_ODBC_VERSION, mas o atributo não tem nenhum efeito sobre a conexão do aplicativo com um ODBC 2. *x* ou ODBC 3. Driver *x* . Um ODBC 3. o aplicativo *x* pode se conectar a um ODBC 2. *x* ou 3. *x* , independentemente da configuração do atributo de ambiente.  
  
 ODBC 3. os aplicativos *x* nunca devem chamar **SQLAllocEnv**. Como resultado, se o Gerenciador de driver receber uma chamada para **SQLAllocEnv**, ele reconhecerá o aplicativo como ODBC 2. *x* aplicativo.  
  
 O atributo SQL_ATTR_ODBC_VERSION afeta três aspectos diferentes de um ODBC 3. comportamento do driver *x* :  
  
-   SQLSTATEs  
  
-   Tipos de dados de Date, time e timestamp  
  
-   O argumento *CatalogName* em **SQLTables** aceita padrões de pesquisa no ODBC 3. *x*, mas não no ODBC 2. *x*  
  
 A configuração do atributo de ambiente SQL_ATTR_ODBC_VERSION não afeta **SQLSetParam** ou **SQLBindParam**. **SQLColAttribute** também não é afetado por esse bit. Embora **SQLColAttribute** retorne atributos que são afetados pela versão do ODBC (tipo de data, precisão, escala e comprimento), o comportamento pretendido é determinado pelo valor do argumento *FieldIdentifier* . Quando *FieldIdentifier* é igual a SQL_DESC_TYPE, **SQLCOLATTRIBUTE** retorna o ODBC 3. códigos *x* para Date, time e timestamp; Quando *FieldIdentifier* é igual a SQL_COLUMN_TYPE, **SQLCOLATTRIBUTE** retorna o ODBC 2. códigos *x* para Date, time e timestamp.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Mapeamentos de SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Alterações de tipo de dados datetime](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
