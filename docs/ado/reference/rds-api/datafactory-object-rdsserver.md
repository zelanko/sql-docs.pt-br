---
title: Objeto DataFactory (RDSServer) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6848dc441e4a163149296f83b85a3c639ffbe331
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707748"
---
# <a name="datafactory-object-rdsserver"></a>Objeto DataFactory (RDSServer)
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Esse objeto de negócios do lado do servidor padrão implementa métodos que fornecem acesso a dados de leitura/gravação a fontes de dados especificado para aplicativos do lado do cliente.  
  
 O **RDSServer.DataFactory** objeto foi projetado como um objeto de automação do lado do servidor que recebe solicitações de cliente. Em uma implementação de Internet, ele reside em um servidor Web e é instanciado pelo componente ADISAPI. O **RDSServer.DataFactory** objeto fornece leitura e acesso de gravação a dados especificado de códigos-fonte, mas não contém nenhuma lógica de regras de validação ou business.  
  
 Se você usar um método que está disponível em ambos os **RDSServer.DataFactory** e [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objetos, o serviço de dados remoto usa o **RDS. DataControl** versão por padrão. O padrão pressupõe um cenário básico de programação, em que o **RDSServer.DataFactory** serve como um objeto de negócios do lado do servidor genérico.  
  
 Se você quiser que seu aplicativo Web para lidar com o processamento do lado do servidor de tarefas específicas, você pode substituir a **RDSServer.DataFactory** com um objeto comercial personalizado.  
  
 Você pode criar objetos de negócios do lado do servidor que chamam a **RDSServer.DataFactory** métodos, tais como [consulta](../../../ado/reference/rds-api/query-method-rds.md) e [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md). Isso é útil se você quiser adicionar funcionalidade a seus objetos comerciais, mas podem aproveitar as tecnologias de serviço remoto de dados existentes.  
  
 O **DataFactory** objeto não é seguro para scripts que são executados no lado do cliente.  
  
 A ID de classe para o **RDSServer.DataFactory** objeto é 9381D8F5-0288-11 D 0-9501-00AA00B911A5.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método CreateObject, do método Query e objeto DataFactory (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


