---
title: Usando o ADO com linguagens de script | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e3e63f9389016dcd7e198d7d09099f94299bd19
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="using-ado-with-scripting-languages"></a>Usando o ADO com linguagens de script
Em um ambiente de script, ADO permite expor dados por meio de scripts do lado do servidor. Nesse cenário, ADO, o provedor OLE DB subjacente que ele usa, e quaisquer outros componentes necessários para fazer referência a um repositório de dados são instalados em um servidor executando o Internet Information Services (IIS). Usando o Active Server Pages (ASP), o ADO é um componente referenciado em um script que pode gerar HTML, por exemplo. Este conteúdo HTML pode ser passado por meio de HTTP para um navegador da Web do cliente. Usando o script, a página da Web pode enviar ações de volta para o script do lado do servidor, permitindo que você atualizar, percorrer ou visualizar dados específicos.  
  
 Antes de usar um objeto ActiveX em uma página da Web, é importante saber se o objeto é seguro para script. Quando um objeto é considerado seguro para script, isso significa que o controle não pode executar qualquer ação prejudicial no computador do usuário e, portanto, pode ser executado sem solicitar a aprovação do usuário. A tabela a seguir lista os objetos do ADO e indica se eles são seguros para script.  
  
|Objeto|É seguro para script?|  
|------------|-------------------------|  
|Conexão do ADO|Sim|  
|Comando ADO|Não|  
|Parâmetro de ADO|Não|  
|Conjunto de registros ADO|Sim|  
|Registro de ADO|Sim|  
|Fluxo de ADO|Sim|  
|Erro de ADO|Não|  
|Catálogo ADOX|Não|  
|Conjunto de células ADOX|Não|  
|DataControl RDS|Sim|  
|DataSpace RDS|Sim|  
|DataFactory do RDS|Não|  
  
 A tabela a seguir lista os provedores incluídos com o Windows DAC/MDAC e indica se eles são seguros para script.  
  
|Provedor|É seguro para script?|  
|--------------|-------------------------|  
|Forma|Sim|  
|Manter|Sim|  
|Remote|Sim|  
|Provedor OLE DB para SQL Server (SQLOLEDB)|Não|  
|Provedor OLE DB para ODBC (MSDASQL)|Não|  
  
## <a name="odbc-data-sources"></a>Fontes de dados ODBC  
 Uma diferença notável entre o código de ADO do script e scripts não é a fonte de dados ODBC, se usado. Para aplicativos não-script, você pode criar um DSN de usuário administrador da fonte de dados ODBC. Para scripts que são executados no IIS, você deve criar um DSN de sistema; Caso contrário, os scripts não reconhece a fonte de dados que você criou. Isso se aplica a qualquer aplicativo de script do ADO usando o Microsoft OLE DB Provider para ODBC por meio do Microsoft IIS.  
  
## <a name="referencing-the-ado-library"></a>Referência de biblioteca do ADO  
 Não aplicável com linguagens de script.  
  
## <a name="handling-events"></a>Manipulação de eventos  
 Não aplicável com linguagens de script.  
  
 Os tópicos a seguir contêm informações mais específicas sobre como usar ADO com linguagens de script:  
  
-   [Programação ADO VBScript](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [Programação ADO JScript](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Usando o ADO com o Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [Usando o ADO com o Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
