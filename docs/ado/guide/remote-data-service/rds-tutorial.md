---
title: Tutorial RDS | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6cfb12781ca9e7387ea8016de581217ddf95f9c1
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="rds-tutorial"></a>Tutorial RDS
Este tutorial ilustra o uso do modelo de programação do RDS para consultar e atualizar uma fonte de dados. Primeiro, ele descreve as etapas necessárias para realizar essa tarefa. Em seguida, o tutorial é repetido no Microsoft® Visual Basic Scripting Edition (com o ADO para Windows Foundation Classes (ADO/WFC)).  
  
 Este tutorial é codificado em idiomas diferentes por dois motivos:  
  
-   A documentação do RDS assume os códigos de leitor no Visual Basic. Isso torna a documentação conveniente para programadores de Visual Basic, mas menos úteis para programadores que usam outras linguagens.  
  
-   Se você não tiver certeza sobre um recurso específico de RDS e você conhece um pouco de outro idioma, você poderá resolver sua pergunta olhando para o mesmo recurso expressado em outro idioma.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="how-the-tutorial-is-presented"></a>Como o Tutorial é apresentado  
 Este tutorial baseia-se no modelo de programação RDS. Ele aborda cada etapa do modelo de programação individualmente. Além disso, ele ilustra cada etapa com um fragmento de código do Visual Basic.  
  
 O exemplo de código é repetido em outras linguagens com a discussão sobre mínimo. Cada etapa em um tutorial de linguagem de programação determinado é marcada com a etapa correspondente no modelo de programação e descritivo tutorial. Use o número da etapa para se referir a discussão no tutorial descritivo.  
  
 O modelo de programação do RDS é mencionado na seção a seguir. Usá-lo como um roteiro conforme você prosseguir com o tutorial.  
  
## <a name="rds-programming-model-with-objects"></a>Modelo de programação de RDS com objetos  
  
-   Especifique o programa a ser invocado no servidor e obter uma forma (proxy) para se referir a ele do cliente.  
  
-   Invoque o programa do servidor. Passe parâmetros para o programa do servidor que identifica a fonte de dados e emitir o comando.  
  
-   O programa de servidor obtém um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto da fonte de dados, normalmente usando o ADO. Opcionalmente, o **registros** objeto for processado no servidor.  
  
-   O programa do servidor retorna o último **registros** objeto para o aplicativo cliente.  
  
-   No cliente, o **registros** objeto opcionalmente é colocado em um formulário que pode ser usado facilmente por controles de visual.  
  
-   Altera para o **registros** objeto são enviadas de volta para o servidor e usado para atualizar a fonte de dados.  
  
 Este tutorial contém os tópicos a seguir.  
  
-   [Etapa 1: Especificar um programa de servidor (Tutorial RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [Etapa 2: Invocar o programa de servidor (Tutorial RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [Etapa 3: O servidor obtém um conjunto de registros (Tutorial RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [Etapa 4: O servidor retorna um conjunto de registros (Tutorial RDS)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [Etapa 5: O DataControl é tornado utilizável (Tutorial RDS)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [Etapa 6: As alterações são enviadas ao servidor (Tutorial RDS)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>Consulte também  
 [Etapa 1: Especificar um programa de servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

