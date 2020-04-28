---
title: Usando o ADO com linguagens de script | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b322dacbf85ec24b58e315ecbbf9d547d1481f9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926485"
---
# <a name="using-ado-with-scripting-languages"></a>Usar o ADO com linguagens de script
Em um ambiente de script, o ADO permite expor dados por meio de scripts do lado do servidor. Nesse cenário, o ADO, o provedor de OLE DB subjacente que ele usa, e quaisquer outros componentes necessários para fazer referência a um determinado repositório de dados são instalados em um servidor que executa o Serviços de Informações da Internet (IIS). Usando páginas de Active Server (ASP), o ADO é um componente referenciado em um script que pode gerar HTML, por exemplo. Esse conteúdo HTML pode ser passado via HTTP para um navegador da Web do cliente. Usando scripts, a página da Web pode enviar ações de volta para o script do lado do servidor, permitindo que você atualize, percorra ou exiba dados específicos.  
  
 Antes de usar um objeto ActiveX em uma página da Web, é importante saber se o objeto é seguro para scripts. Quando um objeto é considerado seguro para scripts, isso significa que o controle não pode executar nenhuma ação prejudicial no computador do usuário e, portanto, pode ser executado sem solicitar a aprovação do usuário. A tabela a seguir lista os objetos ADO e indica se eles são seguros para scripts.  
  
|Objeto|Seguro para scripts?|  
|------------|-------------------------|  
|Conexão ADO|Sim|  
|Comando ADO|Não|  
|Parâmetro ADO|Não|  
|Conjunto de registros ADO|Sim|  
|Registro ADO|Sim|  
|Fluxo do ADO|Sim|  
|Erro de ADO|Não|  
|Catálogo do ADOX|Não|  
|Células ADOX|Não|  
|Controle de datards|Sim|  
|Espaço de DataSpace|Sim|  
|RDS datafactory|Não|  
  
 A tabela a seguir lista os provedores incluídos com o DAC/MDAC do Windows e indica se eles são seguros para scripts.  
  
|Provedor|Seguro para scripts?|  
|--------------|-------------------------|  
|Forma|Sim|  
|Persist|Sim|  
|Remoto|Sim|  
|Provedor de OLE DB para SQL Server (SQLOLEDB)|Não|  
|Provedor de OLE DB para ODBC (MSDASQL)|Não|  
  
## <a name="odbc-data-sources"></a>Fontes de dados ODBC  
 Uma diferença notável entre script e código ADO sem scripts é a fonte de dados ODBC, se usada. Para aplicativos que não são de script, você pode criar um DSN de usuário no administrador de fonte de dados ODBC. Para scripts que estão sendo executados no IIS, você deve criar um DSN de sistema; caso contrário, seus scripts não reconhecerão a fonte de dados que você criou. Isso se aplica a qualquer aplicativo de script do ADO usando o provedor de OLE DB da Microsoft para ODBC por meio do IIS da Microsoft.  
  
## <a name="referencing-the-ado-library"></a>Referenciando a biblioteca do ADO  
 Não aplicável a linguagens de script.  
  
## <a name="handling-events"></a>Manipulação de eventos  
 Não aplicável a linguagens de script.  
  
 Os tópicos a seguir contêm informações mais específicas sobre como usar o ADO com linguagens de script:  
  
-   [Programação ADO VBScript](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [Programação ADO JScript](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Usando o ADO com o Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [Usando o ADO com o Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
