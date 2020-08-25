---
description: Usar o ADO com linguagens de script
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8fd27476f577be4719489bc5ca2e1bfee95c5166
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806495"
---
# <a name="using-ado-with-scripting-languages"></a>Usar o ADO com linguagens de script
Em um ambiente de script, o ADO permite expor dados por meio de scripts do lado do servidor. Nesse cenário, o ADO, o provedor de OLE DB subjacente que ele usa, e quaisquer outros componentes necessários para fazer referência a um determinado repositório de dados são instalados em um servidor que executa o Serviços de Informações da Internet (IIS). Usando páginas de Active Server (ASP), o ADO é um componente referenciado em um script que pode gerar HTML, por exemplo. Esse conteúdo HTML pode ser passado via HTTP para um navegador da Web do cliente. Usando scripts, a página da Web pode enviar ações de volta para o script do lado do servidor, permitindo que você atualize, percorra ou exiba dados específicos.  
  
 Antes de usar um objeto ActiveX em uma página da Web, é importante saber se o objeto é seguro para scripts. Quando um objeto é considerado seguro para scripts, isso significa que o controle não pode executar nenhuma ação prejudicial no computador do usuário e, portanto, pode ser executado sem solicitar a aprovação do usuário. A tabela a seguir lista os objetos ADO e indica se eles são seguros para scripts.  
  
|Objeto|Seguro para scripts?|  
|------------|-------------------------|  
|Conexão ADO|Yes|  
|Comando ADO|No|  
|Parâmetro ADO|No|  
|Conjunto de registros ADO|Yes|  
|Registro ADO|Yes|  
|Fluxo do ADO|Yes|  
|Erro de ADO|No|  
|Catálogo do ADOX|No|  
|Células ADOX|No|  
|Controle de datards|Yes|  
|Espaço de DataSpace|Yes|  
|RDS datafactory|No|  
  
 A tabela a seguir lista os provedores incluídos com o DAC/MDAC do Windows e indica se eles são seguros para scripts.  
  
|Provedor|Seguro para scripts?|  
|--------------|-------------------------|  
|Forma|Yes|  
|Persist|Yes|  
|Remoto|Yes|  
|Provedor de OLE DB para SQL Server (SQLOLEDB)|No|  
|Provedor de OLE DB para ODBC (MSDASQL)|No|  
  
## <a name="odbc-data-sources"></a>Fontes de dados ODBC  
 Uma diferença notável entre script e código ADO sem scripts é a fonte de dados ODBC, se usada. Para aplicativos que não são de script, você pode criar um DSN de usuário no administrador de fonte de dados ODBC. Para scripts que estão sendo executados no IIS, você deve criar um DSN de sistema; caso contrário, seus scripts não reconhecerão a fonte de dados que você criou. Isso se aplica a qualquer aplicativo de script do ADO usando o provedor de OLE DB da Microsoft para ODBC por meio do IIS da Microsoft.  
  
## <a name="referencing-the-ado-library"></a>Referenciando a biblioteca do ADO  
 Não aplicável a linguagens de script.  
  
## <a name="handling-events"></a>Manipulação de eventos  
 Não aplicável a linguagens de script.  
  
 Os tópicos a seguir contêm informações mais específicas sobre como usar o ADO com linguagens de script:  
  
-   [Programação ADO VBScript](./vbscript-ado-programming.md)  
  
-   [Programação ADO JScript](./jscript-ado-programming.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Microsoft ActiveX Data Objects (ADO)](../../microsoft-activex-data-objects-ado.md)   
 [Usando o ADO com o Microsoft Visual Basic](./using-ado-with-microsoft-visual-basic.md)   
 [Usar o ADO com o Microsoft Visual C++](./using-ado-with-microsoft-visual-c.md)