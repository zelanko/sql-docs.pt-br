---
title: O programador ODBC&#39;referência de s | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd729956ee7bb1fccf7a8fceb7a435042df4df7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111190"
---
# <a name="odbc-programmer39s-reference"></a>O programador ODBC&#39;referência de s
O *referência do programador de ODBC* contém as seções a seguir.  
  
-   [O que há de novo no ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md) lista os novos recursos ODBC que foram adicionados no SDK do Windows 8.  
  
-   [Programa ODBC de exemplo](../../odbc/reference/sample-odbc-program.md) apresenta um programa ODBC de exemplo.  
  
-   [Introdução ao ODBC](../../odbc/reference/introduction-to-odbc.md) fornece um breve histórico da linguagem de consulta estruturada e ODBC e informações conceituais sobre a interface do ODBC.  
  
-   [Desenvolvimento de aplicativos](../../odbc/reference/develop-app/developing-applications.md) contém informações sobre como desenvolver aplicativos que usam a interface ODBC e drivers de implementação-lo.  
  
-   [Instalando e configurando Software ODBC](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) fornece informações sobre uma referência de função DLL de instalação e configuração.  
  
-   [Desenvolvendo um Driver ODBC](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) contém informações sobre como escrever um driver.  
  
-   [Referência da API](../../odbc/reference/syntax/odbc-reference.md) contém sintaxe e semânticas informações para todas as funções ODBC.  
  
-   [Apêndices do ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) contêm detalhes técnicos e fazer referência a tabelas de gramática SQL, tipos de dados e códigos de erro ODBC.  
  
## <a name="working-with-the-odbc-documentation"></a>Trabalhando com a documentação do ODBC  
 A interface ODBC é projetada para uso com a linguagem de programação C. Uso da interface ODBC abrange três áreas: Instruções SQL, chamadas de função ODBC e programação em C. Esta documentação pressupõe o seguinte:  
  
-   Conhecimento prático da linguagem de programação C.  
  
-   Dados de Conhecimento geral DBMS e uma familiaridade com o SQL.  
  
 As seguintes convenções tipográficas são usadas.  
  
|Formatar|Usado para|  
|------------|--------------|  
|SELECIONE * DE|Letras maiusculas indicam as instruções SQL, nomes de macro e termos usados no nível de comando do sistema operacional.|  
|`RETCODE SQLFetch(hdbc)`|A fonte com espaçamento uniforme é usada para linhas de comando de exemplo e código do programa.|  
|*argument*|Palavras em itálico indicam argumentos programáticos, informações que o usuário ou o aplicativo deve fornecer ou ênfase do word.|  
|**SQLEndTran**|Em negrito indica que a sintaxe deve ser digitado exatamente como mostrados, incluindo nomes de função.|  
|&#124;|Uma barra vertical separa duas opções mutuamente exclusivas em uma linha de sintaxe.|  
|...|Uma elipse indica que os argumentos podem ser repetidos várias vezes.|  
|. . .|Uma coluna de três pontos indica a continuação do anteriores linhas de código.|  
  
## <a name="about-the-code-examples"></a>Sobre os exemplos de código  
 Os exemplos de código neste guia destinam-se apenas para fins ilustrativos. Porque eles são escritos principalmente para demonstrar os princípios ODBC, eficiência, às vezes, foi definida com o intuito de clareza. Além disso, todas seções de código, às vezes, foram omitidas por motivos de clareza. Isso inclui as definições de funções de não-ODBC (funções cujos nomes não começam com "SQL") e a maioria da manipulação de erro.  
  
 Todos os exemplos de código usam cadeias de caracteres ANSI e o mesmo esquema de banco de dados, que é mostrado no início da [funções de catálogo](../../odbc/reference/develop-app/catalog-functions.md).  
  
## <a name="recommended-reading"></a>Leitura recomendada  
 Para obter mais informações sobre o SQL, os padrões a seguir estão disponíveis:  
  
-   Banco de dados SQL com integridade de aprimoramento, ANSI, ANSI 1989 X3.135-1989 - linguagem.  
  
-   Linguagem de banco de dados – SQL: 9075:1992 X3H2 ANSI e ISO/IEC JTC1/SC21/WG3 (SQL-92).  
  
-   Open Group, gerenciamento de dados: Linguagem de consulta estruturada (SQL), versão 2 (The Open Group, 1996).  
  
 Além de padrões e guias do SQL específicas do fornecedor, muitos livros descrevem SQL, incluindo:  
  
-   Data, J. C., com Darwen, Hugh: *Um guia para o padrão SQL* (Addison-Wesley, 1993).  
  
-   Sandra l, Emerson, Darnovsky, Marcy e Arqueiro com arco, Judith s: *Manual do SQL prático* (Addison-Wesley, 1989).  
  
-   Groff, James r e Weinberg, N. de Paul: *Usando o SQL* (Osborne McGraw-Hill, 1990).  
  
-   Gruber, Martin: *Noções básicas sobre o SQL* (Sybex, 1990).  
  
-   Hursch, Jack l e j Carolyn.: *SQL, a linguagem de consulta estruturada* (guia de livros, 1988).  
  
-   Melton, Jim e Simon, Alan r: *Noções básicas sobre o novo SQL: Um guia completo* (Morgan Kaufmann Publishers, 1993).  
  
-   Pascal, Fabian: *SQL e Noções básicas de relacionais* (M & T livros, 1990).  
  
-   Trimble, J. Harvey, Jr. e Chappell, David: *Uma introdução Visual ao SQL* (Wiley, 1989).  
  
-   Van der Lans, Rick F.: *Introdução ao SQL* (Addison-Wesley, 1988).  
  
-   Vang, Soren: *SQL e bancos de dados relacionais* (Microtrend manuais, 1990).  
  
-   Viescas, John: *Guia de referência rápida para o SQL* (Microsoft Corp., 1989).  
  
 Para obter informações adicionais sobre o processamento de transações, consulte:  
  
-   Cinza, N. de J. e o sistema de dados, Andreas: *Processamento de transações: Conceitos e técnicas* (Morgan Kaufmann Publishers, 1993).  
  
-   Hackathorn, Richard d: *Conectividade de banco de dados empresarial* (Wiley & Sons, 1993).  
  
 Para obter mais informações sobre Interfaces de nível de chamada, os padrões a seguir estão disponíveis:  
  
-   Open Group *gerenciamento de dados: SQL chamada nível CLI (Interface), C451* (Open Group, 1995).  
  
-   ISO/IEC 9075-3:1995, a Interface de nível de chamada (SQL/CLI).  
  
 Para obter informações adicionais sobre ODBC, uma série de livros está disponível, incluindo:  
  
-   Geiger, Kyle: *Dentro do ODBC* (Microsoft Press®, 1995).  
  
-   Gryphon, Robert, Charpentier, Luc, Oelschlager, Jon, Shoemaker, Andrew, cruz, Jim e Lilley, w Albert.: *Usando o ODBC 2* (Que, 1994).  
  
-   Johnston, Tom e Osborne, marque: *Guia de desenvolvedores do ODBC* (Howard W. Sams & Company, 1994).  
  
-   Centro-Norte, Ken: *Programação de Multi-DBMS do Windows: Usando C++, Visual Basic, ODBC, OLE 2 e ferramentas para projetos DBMS* (John Wiley & Sons, Inc., 1995).  
  
-   Stegman, ão Michael., Signore, Robert e Creamer, John: *A solução ODBC, conectividade aberta de banco de dados em ambientes de distribuídos* (McGraw-Hill, 1995).  
  
-   Welch, Keith: *Usando o ODBC 2* (Que, 1994).  
  
-   Whiting, fatura: *Teach Yourself ODBC em 21 dias* (Howard W. Sams & Company, 1994).
