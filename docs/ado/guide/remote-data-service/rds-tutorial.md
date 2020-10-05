---
description: Tutorial RDS
title: Tutorial do RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
author: rothja
ms.author: jroth
ms.openlocfilehash: 70f91e85010abb784291c3c9eca52b9a74ed6286
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721387"
---
# <a name="rds-tutorial"></a>Tutorial RDS
Este tutorial ilustra como usar o modelo de programação RDS para consultar e atualizar uma fonte de dados. Primeiro, ele descreve as etapas necessárias para realizar essa tarefa. Em seguida, o tutorial é repetido no Microsoft® Visual Basic Scripting Edition (apresentando o ADO para classes do Windows Foundation (ADO/WFC)).  
  
 Este tutorial é codificado em idiomas diferentes por dois motivos:  
  
-   A documentação do RDS pressupõe que os códigos de leitor no Visual Basic. Isso torna a documentação conveniente para os programadores de Visual Basic, mas menos útil para programadores que usam outras linguagens.  
  
-   Se você não tiver certeza sobre um recurso RDS específico e souber um pouco de outra linguagem, poderá resolver sua pergunta procurando o mesmo recurso expresso em outro idioma.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="how-the-tutorial-is-presented"></a>Como o tutorial é apresentado  
 Este tutorial se baseia no modelo de programação do RDS. Ele aborda cada etapa do modelo de programação individualmente. Além disso, ele ilustra cada etapa com um fragmento de Visual Basic código.  
  
 O exemplo de código é repetido em outras linguagens com a discussão mínima. Cada etapa em um determinado tutorial da linguagem de programação é marcada com a etapa correspondente no modelo de programação e no tutorial descritivo. Use o número da etapa para consultar a discussão no tutorial descritivo.  
  
 O modelo de programação RDS é indicado na seção a seguir. Use-o como um roteiro ao passar pelo tutorial.  
  
## <a name="rds-programming-model-with-objects"></a>Modelo de programação do RDS com objetos  
  
-   Especifique o programa a ser invocado no servidor e obtenha uma maneira (proxy) para referir-se a ele do cliente.  
  
-   Invocar o programa do servidor. Passe parâmetros para o programa do servidor que identifica a fonte de dados e o comando a ser emitido.  
  
-   O programa de servidor Obtém um objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) da fonte de dados, normalmente usando o ADO. Opcionalmente, o objeto **Recordset** é processado no servidor.  
  
-   O programa de servidor retorna o objeto **Recordset** final para o aplicativo cliente.  
  
-   No cliente, o objeto **Recordset** é opcionalmente inserido em um formulário que pode ser facilmente usado por controles visuais.  
  
-   As alterações no objeto **Recordset** são enviadas de volta para o servidor e usadas para atualizar a fonte de dados.  
  
 Este tutorial contém os tópicos a seguir.  
  
-   [Etapa 1: Especificar um programa de servidor (Tutorial RDS)](./step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [Etapa 2: Invocar o programa de servidor (Tutorial RDS)](./step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [Etapa 3: O servidor obtém um conjunto de registros (Tutorial RDS)](./step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [Etapa 4: O servidor retorna um conjunto de registros (Tutorial RDS)](./step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [Etapa 5: O DataControl é tornado utilizável (Tutorial RDS)](./step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [Etapa 6: As alterações são enviadas ao servidor (Tutorial RDS)](./step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [Tutorial RDS (VBScript)](./rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Etapa 1: especificar um programa de servidor (tutorial RDS)](./step-1-specify-a-server-program-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](./rds-tutorial-vbscript.md)