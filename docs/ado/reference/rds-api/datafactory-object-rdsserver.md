---
description: Objeto DataFactory (RDSServer)
title: Objeto datafactory (RDSServer) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e31d39f0820a485d4954d789fe2dfb398d8490b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91720977"
---
# <a name="datafactory-object-rdsserver"></a>Objeto DataFactory (RDSServer)
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
 Esse objeto comercial padrão do lado do servidor implementa métodos que fornecem acesso de dados de leitura/gravação a fontes de dados especificadas para aplicativos do lado do cliente.  
  
 O objeto **RDSServer. datafactory** é projetado como um objeto de automação do lado do servidor que recebe solicitações do cliente. Em uma implementação da Internet, ela reside em um servidor Web e é instanciada pelo componente ADISAPI. O objeto **RDSServer. datafactory** fornece acesso de leitura e gravação a fontes de dados especificadas, mas não contém nenhuma lógica de validação ou regra de negócio.  
  
 Se você usar um método que esteja disponível no **RDSServer. datafactory** e no [RDS. Objetos DataControl](./datacontrol-object-rds.md) , o serviço de dados remotos usa o **RDS. Versão do DataControl** por padrão. O padrão pressupõe um cenário de programação básico, em que o **RDSServer. datafactory** serve como um objeto de negócios genérico do lado do servidor.  
  
 Se desejar que seu aplicativo Web manipule o processamento do lado do servidor específico da tarefa, você poderá substituir o **RDSServer. datafactory** por um objeto comercial personalizado.  
  
 Você pode criar objetos comerciais do lado do servidor que chamam os métodos **RDSServer. datafactory** , como [Query](./query-method-rds.md) e [createrecordset](./createrecordset-method-rds.md). Isso será útil se você quiser adicionar funcionalidade aos seus objetos comerciais, mas aproveitar as tecnologias de serviço de dados remoto existentes.  
  
 O objeto **DataFactory** não é seguro para scripts executados no lado do cliente.  
  
 A ID de classe do objeto **RDSServer. datafactory** é 9381D8F5-0288-11D0-9501-00AA00B911A5.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto DataFactory (RDSServer)](./datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método CreateObject, do método Query e objeto DataFactory (VBScript)](./datafactory-object-query-method-and-createobject-method-example-vbscript.md)