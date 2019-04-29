---
title: Tutorial RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c9136f1fc1fdf7538744501984af50e2ca52f04
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62929885"
---
# <a name="rds-tutorial"></a>Tutorial RDS
Este tutorial ilustra como usar o modelo de programação do RDS para consultar e atualizar uma fonte de dados. Primeiro, ele descreve as etapas necessárias para realizar essa tarefa. Em seguida, o tutorial é repetido no Microsoft® Visual Basic Scripting Edition (apresentando o ADO para Windows Foundation Classes (ADO/WFC)).  
  
 Este tutorial é codificado em diferentes idiomas por dois motivos:  
  
-   A documentação do RDS pressupõe que os códigos de leitor no Visual Basic. Isso torna a documentação conveniente para programadores de Visual Basic, mas menos úteis para programadores que usam outras linguagens.  
  
-   Se você não tiver certeza sobre um determinado recurso RDS e você sabe um pouco de outro idioma, você poderá resolver sua pergunta olhando para o mesmo recurso expressado em outra linguagem.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="how-the-tutorial-is-presented"></a>Como o Tutorial é apresentado  
 Este tutorial se baseia no modelo de programação do RDS. Ele aborda cada etapa do modelo de programação individualmente. Além disso, ele ilustra cada etapa com um fragmento de código do Visual Basic.  
  
 O exemplo de código é repetido em outras linguagens com mínima discussão. Cada etapa em um tutorial de linguagem de programação determinado é marcada com a etapa correspondente no modelo de programação e tutorial descritivo. Use o número da etapa para referir-se à discussão no tutorial descritivo.  
  
 O modelo de programação do RDS é mencionado na seção a seguir. Usá-lo como um roteiro conforme você continua pelo tutorial.  
  
## <a name="rds-programming-model-with-objects"></a>Modelo de programação do RDS com objetos  
  
-   Especifique o programa a ser invocado no servidor e obter uma maneira (proxy) para se referir a ele do cliente.  
  
-   Invocar o programa do servidor. Passe parâmetros para o programa de servidor que identifica a fonte de dados e emitir o comando.  
  
-   O programa de servidor obtém um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto da fonte de dados, normalmente usando o ADO. Opcionalmente, o **Recordset** objeto for processado no servidor.  
  
-   O programa de servidor retorna o último **Recordset** objeto para o aplicativo cliente.  
  
-   No cliente, o **Recordset** objeto opcionalmente é colocado em um formulário que pode ser facilmente usado por controles visuais.  
  
-   Altera para o **Recordset** objeto são enviadas de volta para o servidor e usado para atualizar a fonte de dados.  
  
 Este tutorial contém os tópicos a seguir.  
  
-   [Etapa 1: Especifique um programa de servidor (Tutorial RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [Etapa 2: Invocar o programa de servidor (Tutorial RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [Etapa 3: Servidor obtém um conjunto de registros (Tutorial RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [Etapa 4: Servidor retorna o conjunto de registros (Tutorial RDS)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [Etapa 5: DataControl é tornado utilizável (Tutorial RDS)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [Etapa 6: As alterações são enviadas ao servidor (Tutorial RDS)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>Consulte também  
 [Etapa 1: Especifique um programa de servidor (Tutorial RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
