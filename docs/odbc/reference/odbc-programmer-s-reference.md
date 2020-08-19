---
description: Referência do programador de ODBC&#39;s
title: Referência do programador de ODBC&#39;s | Microsoft Docs
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
ms.openlocfilehash: 09d79d9a71b1eaeadf6fd649e7433cf5133de403
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428988"
---
# <a name="odbc-programmer39s-reference"></a>Referência do programador de ODBC&#39;s
A *referência do programador de ODBC* contém as seções a seguir.  
  
-   [O que há de novo no ODBC 3,8](../../odbc/reference/what-s-new-in-odbc-3-8.md) lista os novos recursos ODBC que foram adicionados ao SDK do Windows 8.  
  
-   O [programa ODBC de exemplo](../../odbc/reference/sample-odbc-program.md) apresenta um exemplo de programa ODBC.  
  
-   [A introdução ao ODBC](../../odbc/reference/introduction-to-odbc.md) fornece um breve histórico de linguagem SQL e ODBC e informações conceituais sobre a interface ODBC.  
  
-   O [desenvolvimento de aplicativos](../../odbc/reference/develop-app/developing-applications.md) contém informações sobre o desenvolvimento de aplicativos que usam a interface ODBC e os drivers que o implementam.  
  
-   [Instalar e configurar o software ODBC](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) fornece informações sobre a instalação e uma referência de função de DLL de instalação.  
  
-   [O desenvolvimento de um driver ODBC](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) contém informações sobre como gravar um driver.  
  
-   A [referência de API](../../odbc/reference/syntax/odbc-reference.md) contém informações de sintaxe e semântica para todas as funções ODBC.  
  
-   Os [apêndices ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) contêm detalhes técnicos e tabelas de referência para códigos de erro ODBC, tipos de dados e gramática SQL.  
  
## <a name="working-with-the-odbc-documentation"></a>Trabalhando com a documentação ODBC  
 A interface ODBC é projetada para uso com a linguagem de programação C. O uso da interface ODBC abrange três áreas: instruções SQL, chamadas da função ODBC e programação em C. Esta documentação pressupõe o seguinte:  
  
-   Um conhecimento prático da linguagem de programação C.  
  
-   Conhecimento geral do DBMS e familiaridade com o SQL.  
  
 As convenções tipográficas a seguir são usadas.  
  
|Formatar|Usado para|  
|------------|--------------|  
|SELECIONAR * DE|Letras maiúsculas indicam instruções SQL, nomes de macro e termos usados no nível de comando do sistema operacional.|  
|`RETCODE SQLFetch(hdbc)`|A fonte monospace é usada para linhas de comando de exemplo e código de programa.|  
|*argument*|Palavras em itálico indicam argumentos programáticos, informações que o usuário ou o aplicativo deve fornecer ou ênfase de palavras.|  
|**SQLEndTran**|O tipo Bold indica que a sintaxe deve ser digitada exatamente como mostrado, incluindo nomes de função.|  
|&#124;|Uma barra vertical separa duas opções mutuamente exclusivas em uma linha de sintaxe.|  
|...|Uma elipse indica que os argumentos podem ser repetidos várias vezes.|  
|. . .|Uma coluna de três pontos indica a continuação das linhas de código anteriores.|  
  
## <a name="about-the-code-examples"></a>Sobre os exemplos de código  
 Os exemplos de código neste guia são projetados apenas para fins ilustrativos. Como eles são escritos principalmente para demonstrar os princípios de ODBC, às vezes, a eficiência foi reservada no interesse da clareza. Além disso, as seções inteiras de código, às vezes, foram omitidas para maior clareza. Isso inclui as definições de funções não-ODBC (as funções cujos nomes não começam com "SQL") e a maioria do tratamento de erros.  
  
 Todos os exemplos de código usam cadeias de caracteres ANSI e o mesmo esquema de banco de dados, que é mostrado no início das [funções de catálogo](../../odbc/reference/develop-app/catalog-functions.md).  
  
## <a name="recommended-reading"></a>Leitura recomendada  
 Para obter mais informações sobre o SQL, os seguintes padrões estão disponíveis:  
  
-   Linguagem de banco de dados-SQL com aprimoramento de integridade, ANSI, 1989 ANSI X 3.135-1989.  
  
-   Linguagem de banco de dados-SQL: ANSI X3H2 e ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92).  
  
-   Abra grupo, Gerenciamento de Dados: linguagem SQL (SQL), versão 2 (o grupo aberto, 1996).  
  
 Além dos padrões e dos guias SQL específicos do fornecedor, muitos livros descrevem o SQL, incluindo:  
  
-   Data, C. J., com Darwen, Hugh: *um guia para o SQL Standard* (Addison-Wesley, 1993).  
  
-   Emerson, Sandra L., Darnovsky, Marcy e Bowman, Judith S.: *o manual do SQL prático* (Addison-Wesley, 1989).  
  
-   Groff, James R. e Weinberg, Paul N.: *usando SQL* (Osborne McGraw-Hill, 1990).  
  
-   Gruber, Martin: *Understanding SQL* (Sybex, 1990).  
  
-   Hursch, Jack L. e Carolyn J.: *SQL, a linguagem SQL* (livros de guias, 1988).  
  
-   Melton, Jim e Simon, Alan R.: *noções básicas sobre o novo SQL: um guia completo* (Morgan Kaufmann Publishers, 1993).  
  
-   Pascal, Fabian: *SQL e noções básicas relacionais* (M & livros T, 1990).  
  
-   Trimble, J. Harvey, Jr. e Chappell, David: *uma introdução visual ao SQL* (Wiley, 1989).  
  
-   Van der LANs, Rick F.: *Introduction to SQL* (Addison-Wesley, 1988).  
  
-   Vang, Soren: *SQL e bancos de dados relacionais* (livros de microtendência, 1990).  
  
-   Viescas, John: *Guia de referência rápida para SQL* (Microsoft Corp., 1989).  
  
 Para obter informações adicionais sobre o processamento de transações, consulte:  
  
-   Cinza, J. N. e Reuter, Andreas: *processamento de transações: conceitos e técnicas* (Morgan Kaufmann Publishers, 1993).  
  
-   Hackathorn, Richard D.: *conectividade de banco de dados empresarial* (Wiley & filhos, 1993).  
  
 Para obter mais informações sobre interfaces de nível de chamada, os seguintes padrões estão disponíveis:  
  
-   Abrir grupo, *Gerenciamento de dados: CLI (interface de nível de chamada) do SQL, C451* (grupo aberto, 1995).  
  
-   ISO/IEC 9075-3:1995, interface de nível de chamada (SQL/CLI).  
  
 Para obter informações adicionais sobre ODBC, há vários livros disponíveis, incluindo:  
  
-   Geiger, Kyle: *Inside ODBC* (Microsoft Press®, 1995).  
  
-   Gryphon, Robert, Charpentier, Luc, Oelschlager, Jon, Shoemaker, Andrew, Cross, Jim e Lilley, Albert W.: *usando ODBC 2* (que é 1994).  
  
-   Johnston, Tom e Osborne, Mark: *Guia de desenvolvedores de ODBC* (Howard W. Sams & Company, 1994).  
  
-   Norte, Ken: *programação de vários DBMS do Windows: usando C++, Visual Basic, ODBC, OLE 2 e ferramentas para projetos DBMS* (John Wiley & filhos, Inc., 1995).  
  
-   Stegman, Michael O., Signore, Robert e sorvete, João: *a solução ODBC, Open Database Connectivity em ambientes distribuídos* (McGraw-Hill, 1995).  
  
-   Welch, Keith: *usando ODBC 2* (que é 1994).  
  
-   Whiting, Bill: *Ensine-se ao ODBC em vinte a um dias* (Howard W. Sams & Company, 1994).
