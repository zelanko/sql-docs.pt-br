---
title: Exemplo de SQL inserido | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 966962bdda79a57e83a0bce06b9254267efb474c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068665"
---
# <a name="embedded-sql-example"></a>Exemplo de SQL inserido
O código a seguir é um programa simples incorporado do SQL, escrito em C. O programa ilustra muitas, mas não todas, as técnicas de SQL inseridas. O programa solicita ao usuário um número de pedido, recupera o número do cliente, o vendedor e o status do pedido e exibe as informações recuperadas na tela.  
  
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
  
-   **Variáveis de host** As variáveis de host são declaradas em uma seção delimitada pelas palavras-chave **begin declare section** e **end declare section** . Cada nome de variável de host é prefixado por dois-pontos (:) Quando ele aparece em uma instrução SQL inserida. Os dois-pontos permitem que o pré-compilador Diferencie entre variáveis de host e objetos de banco de dados, como tabelas e colunas, que têm o mesmo nome.  
  
-   **Tipos de dados** Os tipos de dados com suporte de um DBMS e um idioma de host podem ser bem diferentes. Isso afeta as variáveis de host porque elas desempenham uma função dupla. Por um lado, as variáveis de host são variáveis de programa, declaradas e manipuladas por instruções de idioma do host. Por outro lado, eles são usados em instruções SQL inseridas para recuperar dados do banco de dados. Se não houver nenhum tipo de idioma do host que corresponda a um tipo de dados DBMS, o DBMS converterá automaticamente os dados. No entanto, como cada DBMS tem suas próprias regras e idiossincrasias associadas ao processo de conversão, os tipos de variáveis de host devem ser escolhidos com cuidado.  
  
-   **Tratamento de erro** O DBMS relata erros de tempo de execução para o programa aplicativos por meio de uma área de comunicações SQL ou SQLCA. No exemplo de código anterior, a primeira instrução SQL inserida é incluir SQLCA. Isso informa o pré-compilador para incluir a estrutura SQLCA no programa. Isso é necessário sempre que o programa processar erros retornados pelo DBMS. O sempre... A instrução GOTO informa o pré-compilador para gerar o código de tratamento de erros que ramifica para um rótulo específico quando ocorre um erro.  
  
-   **Seleção de singleton** A instrução usada para retornar os dados é uma instrução SELECT singleton; ou seja, ele retorna apenas uma única linha de dados. Portanto, o exemplo de código não declara nem usa cursores.
