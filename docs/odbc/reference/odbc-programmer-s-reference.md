---
title: ODBC programador referência de | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b934652505039a021d2b08c0fa5314614ce9c609
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-programmer39s-reference"></a>O programador ODBC referência
O *referência do programador de ODBC* contém as seções a seguir.  
  
-   [O que há de novo no ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md) lista os novos recursos ODBC que foram incluídos no SDK do Windows 8.  
  
-   [Exemplo de programa ODBC](../../odbc/reference/sample-odbc-program.md) apresenta um programa de exemplo ODBC.  
  
-   [Introdução ao ODBC](../../odbc/reference/introduction-to-odbc.md) fornece um breve histórico de Structured Query Language, ODBC e informações conceituais sobre a interface do ODBC.  
  
-   [Desenvolvendo aplicativos](../../odbc/reference/develop-app/developing-applications.md) contém informações sobre como desenvolver aplicativos que usam a interface ODBC e drivers de implementação-la.  
  
-   [Instalando e configurando Software ODBC](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) fornece informações sobre uma referência de função DLL de instalação e configuração.  
  
-   [Desenvolvendo um Driver ODBC](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) contém informações sobre como escrever um driver.  
  
-   [Referência da API](../../odbc/reference/syntax/odbc-reference.md) contém sintaxe e semânticas informações para todas as funções ODBC.  
  
-   [Apêndices ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) contêm detalhes técnicos e fazer referência a tabelas de gramática de SQL, tipos de dados e códigos de erro ODBC.  
  
## <a name="working-with-the-odbc-documentation"></a>Trabalhando com a documentação do ODBC  
 A interface ODBC foi projetada para uso com a linguagem de programação C. Uso da interface ODBC abrange três áreas: instruções SQL, ODBC função chamadas e programação C. Esta documentação pressupõe o seguinte:  
  
-   Conhecimento prático da linguagem de programação C.  
  
-   O conhecimento de DBMS geral e uma familiaridade com o SQL.  
  
 As seguintes convenções tipográficas são usadas.  
  
|Formato|Usado para|  
|------------|--------------|  
|SELECIONE * DE|Letras maiusculas indicam instruções SQL, nomes de macro e termos usados no nível de comando do sistema operacional.|  
|`RETCODE SQLFetch(hdbc)`|A fonte de espaçamento uniforme é usada para linhas de comando de exemplo e código de programa.|  
|*argumento*|Palavras em itálico indicam argumentos programáticos, informações que o usuário ou o aplicativo deve fornecer ou word ênfase.|  
|**SQLEndTran**|Em negrito indica sintaxe deve ser digitada exatamente conforme mostrado, incluindo nomes de função.|  
|&#124;|Uma barra vertical separa as duas opções mutuamente exclusivas em uma linha de sintaxe.|  
|...|Uma elipse indica que os argumentos podem ser repetidos várias vezes.|  
|para obter informações sobre a ferramenta de configuração e recursos adicionais. para obter informações sobre a ferramenta de configuração e recursos adicionais. para obter informações sobre a ferramenta de configuração e recursos adicionais.|Uma coluna de três pontos indica continuação anterior linhas de código.|  
  
## <a name="about-the-code-examples"></a>Sobre os exemplos de código  
 Os exemplos de código neste guia destinam-se apenas para fins ilustrativos. Porque eles são gravados principalmente para demonstrar os princípios ODBC, eficiência, às vezes, foi definida para fins de esclarecimento. Além disso, todas seções do código, às vezes, foram omitidas para fins de esclarecimento. Isso inclui as definições de funções de ODBC não (funções cujos nomes não começam com "SQL") e a maioria dos tratamento de erros.  
  
 Todos os exemplos de código usam cadeias de caracteres ANSI e o mesmo esquema de banco de dados, que é mostrado no início de [funções de catálogo](../../odbc/reference/develop-app/catalog-functions.md).  
  
## <a name="recommended-reading"></a>Leitura recomendada  
 Para obter mais informações sobre SQL, os padrões a seguir estão disponíveis:  
  
-   Idioma do banco de dados — SQL com integridade de aprimoramento, ANSI, ANSI 1989 X3.135-1989.  
  
-   Idioma do banco de dados — SQL: X3H2 ANSI e ISO/IEC 9075:1992 SC21/JTC1/WG3 (SQL-92).  
  
-   Open Group, gerenciamento de dados: Linguagem de consulta estruturada (SQL), versão 2 (The Open Group, 1996).  
  
 Além dos padrões e guias SQL específicas do fornecedor, muitos livros descrevem SQL, incluindo:  
  
-   Data, J. C., com Darwen, Hugh: *um guia para o padrão SQL* (Addison-Wesley, 1993).  
  
-   Emerson, Sandra l, Darnovsky, Marcy e Arqueiro com arco, Judith s: *o manual do SQL prático* (Addison-Wesley, 1989).  
  
-   Groff, James r e Weinberg, Paul n: *usando SQL* (Osborne McGraw-monte, 1990).  
  
-   Gruber, Martin: *Noções básicas sobre SQL* (Sybex, 1990).  
  
-   Hursch, L. o conector e j Carolyn: *SQL, a linguagem de consulta estruturada* (guia de livros, 1988).  
  
-   Melton, Jim e Simon, Alan r: *Noções básicas sobre o novo SQL: um guia completo* (editores de Morgan Kaufmann, 1993).  
  
-   Pascal, Fabian: *SQL e Noções básicas sobre relacional* (M & T manuais, 1990).  
  
-   Trimble, J. Harvey, Jr e Chappell, David: *uma Visual Introdução ao SQL* (1989 Wiley,).  
  
-   Van der Lans, Rick F.: *Introdução ao SQL* (Addison-Wesley, 1988).  
  
-   Vang, Soren: *SQL e bancos de dados relacionais* (Microtrend manuais, 1990).  
  
-   Viescas, João: *guia de referência rápida para o SQL* (Microsoft Corp., 1989).  
  
 Para obter informações adicionais sobre o processamento de transações, consulte:  
  
-   Cinza, n J. e sistema de dados, Andreas: *processamento de transações: conceitos e técnicas* (editores de Morgan Kaufmann, 1993).  
  
-   Hackathorn, Richard d: *conectividade de banco de dados da empresa* (Wiley & Sons, 1993).  
  
 Para obter mais informações sobre as Interfaces de nível de chamada, os padrões a seguir estão disponíveis:  
  
-   Open Group *gerenciamento de dados: SQL chamada nível CLI (Interface), C451* (Open Group, 1995).  
  
-   ISO/IEC 9075-3:1995, a Interface de nível de chamada (SQL/CLI).  
  
 Para obter informações adicionais sobre ODBC, um número de livros está disponível, incluindo:  
  
-   Geiger, Kyle: *dentro de ODBC* (Microsoft Press®, 1995).  
  
-   Gryphon, Robert, Charpentier, Luc, Oelschlager, Carlos, Shoemaker, Andrew, cruz, Jim e Lilley, w Albert: *usando o ODBC 2* (Que, 1994).  
  
-   Johnston, Tom e Osborne, marcar: *guia do desenvolvedor do ODBC* (Howard W. Sams & empresa, 1994).  
  
-   Norte, Ken: *Windows Multi-DBMS programação: usando C++, Visual Basic, ODBC, OLE 2 e ferramentas para projetos DBMS* (John Wiley & Sons, Inc., 1995).  
  
-   Stegman ão Michael., Signore, Robert e Creamer, João: *a solução ODBC, conectividade aberta de banco de dados em ambientes distribuídos* (McGraw monte, 1995).  
  
-   Welch, Keith: *usando o ODBC 2* (Que, 1994).  
  
-   Whiting, fatura: *Aprenda ODBC em 21 dias* (Howard W. Sams & empresa, 1994).
