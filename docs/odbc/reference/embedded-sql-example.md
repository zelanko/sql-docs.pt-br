---
title: Exemplo sql incorporado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39ec504c423817c6a3e11bc954555b201b8b09c6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294167"
---
# <a name="embedded-sql-example"></a>Exemplo de SQL inserido
O código a seguir é um simples programa SQL incorporado, escrito em C. O programa ilustra muitas, mas não todas, das técnicas sql incorporadas. O programa solicita ao usuário um número de pedido, recupera o número do cliente, o vendedor e o status do pedido e exibe as informações recuperadas na tela.  
  
```cpp  
int main() {  
   EXEC SQL INCLUDE SQLCA;  
   EXEC SQL BEGIN DECLARE SECTION;  
      int OrderID;         /* Employee ID (from user)         */  
      int CustID;            /* Retrieved customer ID         */  
      char SalesPerson[10]   /* Retrieved salesperson name      */  
      char Status[6]         /* Retrieved order status        */  
   EXEC SQL END DECLARE SECTION;  
  
   /* Set up error processing */  
   EXEC SQL WHENEVER SQLERROR GOTO query_error;  
   EXEC SQL WHENEVER NOT FOUND GOTO bad_number;  
  
   /* Prompt the user for order number */  
   printf ("Enter order number: ");  
   scanf_s("%d", &OrderID);  
  
   /* Execute the SQL query */  
   EXEC SQL SELECT CustID, SalesPerson, Status  
      FROM Orders  
      WHERE OrderID = :OrderID  
      INTO :CustID, :SalesPerson, :Status;  
  
   /* Display the results */  
   printf ("Customer number:  %d\n", CustID);  
   printf ("Salesperson: %s\n", SalesPerson);  
   printf ("Status: %s\n", Status);  
   exit();  
  
query_error:  
   printf ("SQL error: %ld\n", sqlca->sqlcode);  
   exit();  
  
bad_number:  
   printf ("Invalid order number.\n");  
   exit();  
}  
```  
  
 Observe o seguinte sobre este programa:  
  
-   **Variáveis de host** As variáveis host são declaradas em uma seção fechada pelas palavras-chave **BEGIN DECLARE SECTION** e END DECLARE **SECTION.** Cada nome variável do host é prefixado por um cólon (:) quando ele aparece em uma declaração SQL incorporada. O cólon permite que o pré-compilador diferencie entre variáveis de host e objetos de banco de dados, como tabelas e colunas, que tenham o mesmo nome.  
  
-   **Tipos de dados** Os tipos de dados suportados por um DBMS e uma linguagem host podem ser bem diferentes. Isso afeta as variáveis do host porque elas desempenham um papel duplo. Por um lado, as variáveis do host são variáveis do programa, declaradas e manipuladas por declarações de idioma host. Por outro lado, eles são usados em declarações SQL incorporadas para recuperar dados do banco de dados. Se não houver um tipo de idioma host correspondente a um tipo de dados DBMS, o DBMS converte automaticamente os dados. No entanto, como cada DBMS tem suas próprias regras e idiossincrasias associadas ao processo de conversão, os tipos de variáveis host devem ser escolhidos cuidadosamente.  
  
-   **Manipulação de erros** O DBMS relata erros de tempo de execução para o programa de aplicativos através de uma Área de Comunicações SQL, ou SQLCA. No exemplo de código anterior, a primeira declaração SQL incorporada é INCLUDE SQLCA. Isso diz ao pré-compilador para incluir a estrutura SQLCA no programa. Isso é necessário sempre que o programa processará erros retornados pelo DBMS. O SEMPRE... A instrução GOTO informa ao pré-compilador para gerar código de manipulação de erros que se ramifica a um rótulo específico quando ocorre um erro.  
  
-   **Singleton SELECT** A declaração usada para retornar os dados é uma declaração singleton SELECT; ou seja, ele retorna apenas uma única linha de dados. Portanto, o exemplo de código não declara ou usa cursores.
