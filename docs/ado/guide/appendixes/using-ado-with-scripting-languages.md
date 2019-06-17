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
manager: jroth
ms.openlocfilehash: d41d5a0239f11882c135c27fd4af8e817e83b799
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702770"
---
# <a name="using-ado-with-scripting-languages"></a>Usar o ADO com linguagens de script
Dentro de um ambiente de script, o ADO permite que você exponha os dados por meio de scripts do lado do servidor. Nesse cenário, o ADO, o provedor OLE DB subjacente que ele usa, e todos os outros componentes necessários para fazer referência a um repositório de dados fornecidos são instalados em um servidor executando o Internet Information Services (IIS). Usando o Active Server Pages (ASP), o ADO é um componente referenciado em um script que pode gerar HTML, por exemplo. Esse conteúdo HTML pode ser passado por meio de HTTP para um navegador da Web de cliente. Usando scripts, a página da Web pode enviar ações de volta para o script do lado do servidor, permitindo que você atualizar, percorrer ou exibir dados específicos.  
  
 Antes de usar um objeto ActiveX em uma página da Web, é importante saber se o objeto é seguro para script. Quando um objeto é considerado seguro para script, isso significa que o controle não pode executar qualquer ação prejudicial no computador do usuário e, portanto, pode ser executado sem solicitar a aprovação do usuário. A tabela a seguir lista os objetos do ADO e indica se eles são seguros para script.  
  
|Object|É seguro para execução de scripts?|  
|------------|-------------------------|  
|Conexão do ADO|Sim|  
|Comando ADO|Não|  
|Parâmetro ADO|Não|  
|ADO Recordset|Sim|  
|ADO Record|Sim|  
|ADO Stream|Sim|  
|Erro de ADO|Não|  
|Catálogo do ADOX|Não|  
|Conjunto de células do ADOX|Não|  
|DataControl RDS|Sim|  
|Espaço de dados do RDS|Sim|  
|RDS DataFactory|Não|  
  
 A tabela a seguir lista os provedores incluídos com o Windows DAC/MDAC e indica se eles são seguros para script.  
  
|Provedor|É seguro para execução de scripts?|  
|--------------|-------------------------|  
|Forma|Sim|  
|Persistir|Sim|  
|Remote|Sim|  
|Provedor OLE DB para SQL Server (SQLOLEDB)|Não|  
|Provedor OLE DB para ODBC (MSDASQL)|Não|  
  
## <a name="odbc-data-sources"></a>Fontes de dados ODBC  
 Uma diferença importante entre o código ADO de script e scripts não é a fonte de dados ODBC, se usado. Para aplicativos não-script, você pode criar um DSN de usuário no administrador de fonte de dados ODBC. Para scripts que são executados no IIS, você deve criar um DSN de sistema; Caso contrário, os scripts não reconhecerá a fonte de dados que você criou. Isso se aplica a qualquer aplicativo de script do ADO usando o Microsoft OLE DB Provider para ODBC por meio do Microsoft IIS.  
  
## <a name="referencing-the-ado-library"></a>Referência à biblioteca do ADO  
 Não aplicável com linguagens de script.  
  
## <a name="handling-events"></a>Manipulação de eventos  
 Não aplicável com linguagens de script.  
  
 Os tópicos a seguir contêm informações mais específicas sobre como usar o ADO com linguagens de script:  
  
-   [Programação ADO VBScript](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [Programação ADO JScript](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Usando o ADO com o Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [Usando o ADO com o Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
