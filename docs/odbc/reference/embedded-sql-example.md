---
title: Embedded SQL de exemplo | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: eef8c87a152795d4756d05ba8a279a0d12cbc38c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628610"
---
# <a name="embedded-sql-example"></a>Exemplo de SQL inserido
O código a seguir é um programa SQL inserido simples, escrito em C. O programa ilustra muitas, mas não todas, do embedded técnicas do SQL. O programa solicita ao usuário um número de pedido, recupera o número do cliente, o vendedor e o status do pedido e exibe as informações recuperadas na tela.  
  
```  
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
  
-   **Variáveis de host** as variáveis de host são declaradas em uma seção delimitada pela **seção DECLARAR começar** e **END DECLARAR seção** palavras-chave. Cada nome de variável do host é prefixado por dois-pontos (:) quando ele for exibido em uma instrução SQL incorporada. Os dois-pontos permite o pré-compilador distinguir entre as variáveis de host e objetos de banco de dados, como tabelas e colunas, que têm o mesmo nome.  
  
-   **Tipos de dados** os tipos de dados compatíveis com um DBMS e uma linguagem de host podem ser bastante diferentes. Isso afeta as variáveis do host porque eles desempenham um papel de duplo. Por um lado, as variáveis de host são variáveis de programa, declarado e manipulados por instruções de linguagem do host. Por outro lado, eles são usados em instruções inseridas do SQL para recuperar o banco de dados. Se não houver nenhum tipo de linguagem de host que corresponde a um tipo de dados do DBMS, o DBMS converte automaticamente os dados. No entanto, como cada DBMS tem suas próprias regras e Idiossincrasias associadas com o processo de conversão, os tipos de variáveis do host devem ser cuidadosamente escolhidos.  
  
-   **Tratamento de erro** o DBMS relata erros de tempo de execução do programa de aplicativos por meio de uma área de comunicações do SQL, ou SQLCA. No exemplo de código anterior, a primeira instrução de SQL inserida é incluir SQLCA. Isso informa o pré-compilador para incluir a estrutura SQLCA no programa. Isso é necessário sempre que o programa irá processar erros retornados pelo DBMS. WHENEVER... Instrução GOTO informa o pré-compilador para gerar o código de tratamento de erros que ramificações para um rótulo específico quando um erro ocorre.  
  
-   **Singleton selecione** a instrução usada para retornar os dados é uma instrução SELECT de singleton; ou seja, ele retorna apenas uma única linha de dados. Portanto, o exemplo de código não declarar ou usar cursores.
