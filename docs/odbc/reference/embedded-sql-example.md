---
title: Inserido exemplo SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d8983bcabb791c99974055fa718bdd89057e2d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916351"
---
# <a name="embedded-sql-example"></a>Exemplo SQL incorporado
O código a seguir é um programa SQL incorporado simple, escrito em C. O programa ilustra muitas, mas não em todas as incorporado técnicas do SQL. O programa solicita ao usuário um número de pedido, recupera o número do cliente, o vendedor e o status do pedido e exibe as informações recuperadas na tela.  
  
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
  
-   **Variáveis de host** as variáveis de host são declaradas em uma seção entre o **começar DECLARAR seção** e **final DECLARAR seção** palavras-chave. Cada nome de variável do host é prefixado por dois-pontos (:) quando ele aparece em uma instrução SQL incorporada. Os dois pontos permite o pré-compilador distinguir entre as variáveis do host e objetos de banco de dados, como tabelas e colunas, que têm o mesmo nome.  
  
-   **Tipos de dados** os tipos de dados com suporte por um DBMS e uma linguagem de host podem ser bastante diferentes. Isso afeta a variáveis de host porque eles têm uma função dupla. Por um lado, variáveis de host são variáveis de programa, declarado e manipulados por instruções de linguagem host. Por outro lado, eles são usados nas instruções do embedded SQL para recuperar dados do banco de dados. Se não houver nenhum tipo de idioma do host que corresponde a um tipo de dados do DBMS, o DBMS converte automaticamente os dados. No entanto, como cada DBMS tem suas próprias regras e Idiossincrasias associadas com o processo de conversão, os tipos de variável do host devem ser escolhidos com cuidado.  
  
-   **Tratamento de erros** o DBMS relata erros de tempo de execução do programa de aplicativos por meio de uma área de comunicações do SQL, ou SQLCA. No exemplo de código anterior, a primeira instrução SQL inserida é incluir SQLCA. Isso informa o pré-compilador para incluir a estrutura SQLCA no programa. Isso é necessário sempre que o programa processará os erros retornados pelo DBMS. WHENEVER... Instrução GOTO informa o pré-compilador para gerar o código de tratamento de erros que ramificações para um rótulo específico quando um erro ocorre.  
  
-   **Singleton selecione** a instrução usada para retornar os dados é uma instrução SELECT singleton; ou seja, ele retorna somente uma única linha de dados. Portanto, o exemplo de código não declarar ou usar cursores.
