---
title: ODBC Programadora&#39;de Referência | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a9ca32627b9703465dcfca554fdc32ae01442e7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280506"
---
# <a name="odbc-programmer39s-reference"></a>O Programador da ODBC&#39;s Reference
A *Referência do Programador ODBC* contém as seguintes seções.  
  
-   [O que há de novo no ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md) lista os novos recursos do ODBC que foram adicionados no Windows 8 SDK.  
  
-   [O Programa Amostra ODBC](../../odbc/reference/sample-odbc-program.md) apresenta um programa de amostra ODBC.  
  
-   [A introdução ao ODBC](../../odbc/reference/introduction-to-odbc.md) fornece uma breve história da Linguagem de Consulta Estruturada e ODBC, e informações conceituais sobre a interface ODBC.  
  
-   [O desenvolvimento de aplicativos](../../odbc/reference/develop-app/developing-applications.md) contém informações sobre o desenvolvimento de aplicativos que usam a interface ODBC e drivers que a implementam.  
  
-   [Instalação e configuração do software ODBC](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) fornece informações sobre a instalação e uma referência de função DLL de configuração.  
  
-   [O desenvolvimento de um Driver ODBC](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) contém informações sobre como escrever um driver.  
  
-   [A API Reference](../../odbc/reference/syntax/odbc-reference.md) contém informações sintaxe e semântica para todas as funções ODBC.  
  
-   [Os apêndices ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) contêm detalhes técnicos e tabelas de referência para códigos de erro ODBC, tipos de dados e gramática SQL.  
  
## <a name="working-with-the-odbc-documentation"></a>Trabalhando com a Documentação ODBC  
 A interface ODBC é projetada para uso com a linguagem de programação C. O uso da interface ODBC abrange três áreas: instruções SQL, chamadas da função ODBC e programação em C. Esta documentação assume o seguinte:  
  
-   Um conhecimento de trabalho da linguagem de programação C.  
  
-   Conhecimento Geral DBMS e familiaridade com SQL.  
  
 São utilizadas as seguintes convenções tipográficas.  
  
|Formatar|Usado para|  
|------------|--------------|  
|SELECIONE * DE|As letras maiúsculas indicam instruções SQL, nomes de macro e termos usados no nível de comando do sistema operacional.|  
|`RETCODE SQLFetch(hdbc)`|A fonte monoespaço é usada para linhas de comando de amostra e código do programa.|  
|*Argumento*|Palavras itálicas indicam argumentos programáticos, informações que o usuário ou o aplicativo devem fornecer, ou ênfase de palavras.|  
|**SQLEndTran**|O tipo em negrito indica que a sintaxe deve ser digitada exatamente como mostrado, incluindo nomes de função.|  
|&#124;|Uma barra vertical separa duas opções mutuamente exclusivas em uma linha de sintaxe.|  
|...|Uma elipse indica que os argumentos podem ser repetidos várias vezes.|  
|. . .|Uma coluna de três apontamentos indica a continuação de linhas de código anteriores.|  
  
## <a name="about-the-code-examples"></a>Sobre os Exemplos de Código  
 Os exemplos de código neste guia são projetados apenas para fins de ilustração. Por serem escritos principalmente para demonstrar os princípios da ODBC, a eficiência às vezes foi deixada de lado no interesse da clareza. Além disso, seções inteiras de código foram às vezes omitidas para clareza. Estas incluem as definições de funções não-ODBC (aquelas funções cujos nomes não começam com "SQL") e a maior parte do manuseio de erros.  
  
 Todos os exemplos de código usam strings ANSI e o mesmo esquema de banco de dados, que é mostrado no início das [Funções](../../odbc/reference/develop-app/catalog-functions.md)de Catálogo .  
  
## <a name="recommended-reading"></a>Leitura recomendada  
 Para obter mais informações sobre o SQL, as seguintes normas estão disponíveis:  
  
-   Linguagem de banco de dados - SQL com Aprimoramento de Integridade, ANSI, 1989 ANSI X3.135-1989.  
  
-   Linguagem do banco de dados - SQL: ANSI X3H2 e ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92).  
  
-   Grupo Aberto, Gerenciamento de Dados: Linguagem de Consulta Estruturada (SQL), Versão 2 (The Open Group, 1996).  
  
 Além de padrões e guias SQL específicos para fornecedores, muitos livros descrevem sql, incluindo:  
  
-   Data, C. J., com Darwen, Hugh: *A Guide to the SQL Standard* (Addison-Wesley, 1993).  
  
-   Emerson, Sandra L., Darnovsky, Marcy, e Bowman, Judith S.: *The Practical SQL Handbook* (Addison-Wesley, 1989).  
  
-   Groff, James R. e Weinberg, Paul N.: *Usando SQL* (Osborne McGraw-Hill, 1990).  
  
-   Gruber, Martin: *Entendendo SQL* (Sybex, 1990).  
  
-   Hursch, Jack L. e Carolyn J.: *SQL, The Structured Query Language* (TAB Books, 1988).  
  
-   Melton, Jim e Simon, Alan R.: *Understanding the New SQL: A Complete Guide* (Morgan Kaufmann Publishers, 1993).  
  
-   Pascal, Fabian: *SQL e BaseS Relacionais* (M & T Books, 1990).  
  
-   Trimble, J. Harvey Jr. e Chappell, David: *A Visual Introduction to SQL* (Wiley, 1989).  
  
-   Van der Lans, Rick F.: *Introdução ao SQL* (Addison-Wesley, 1988).  
  
-   Vang, Soren: *SQL e Bancos de Dados Relacionais* (Microtrend Books, 1990).  
  
-   Viescas, John: *Guia de Referência Rápida para SQL* (Microsoft Corp., 1989).  
  
 Para obter informações adicionais sobre processamento de transações, consulte:  
  
-   Gray, J.N. e Reuter, Andreas: *Processamento de Transações: Conceitos e Técnicas* (Morgan Kaufmann Publishers, 1993).  
  
-   Hackathorn, Richard D.: *Enterprise Database Connectivity* (Wiley & Sons, 1993).  
  
 Para obter mais informações sobre interfaces de nível de chamada, os seguintes padrões estão disponíveis:  
  
-   Grupo aberto, *gerenciamento de dados: Interface de Nível de Chamada SQL (CLI), C451* (Open Group, 1995).  
  
-   ISO/IEC 9075-3:1995, interface de nível de chamada (SQL/CLI).  
  
 Para obter informações adicionais sobre o ODBC, vários livros estão disponíveis, incluindo:  
  
-   Geiger, Kyle: *Inside ODBC* (Microsoft Press®, 1995).  
  
-   Grifo, Robert, Charpentier, Luc, Oelschlager, Jon, Shoemaker, Andrew, Cross, Jim, e Lilley, Albert W.: *Usando ODBC 2* (Que, 1994).  
  
-   Johnston, Tom e Osborne, Mark: *ODBC Developers Guide* (Howard W. Sams & Company, 1994).  
  
-   North, Ken: *Windows Multi-DBMS Programming: Usando C++, Visual Basic, ODBC, OLE 2 e Tools for DBMS Projects* (John Wiley & Sons, Inc., 1995).  
  
-   Stegman, Michael O., Signore, Robert, and Creamer, John: *The ODBC Solution, Open Database Connectivity in Distributed Environments* (McGraw-Hill, 1995).  
  
-   Welch, Keith: *Usando ODBC 2* (Que, 1994).  
  
-   Whiting, Bill: *Teach Yourself ODBC in Twenty-One Days* (Howard W. Sams & Company, 1994).
