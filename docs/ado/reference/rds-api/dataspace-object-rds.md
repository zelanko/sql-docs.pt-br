---
description: Objeto DataSpace (RDS)
title: Objeto DataSpace (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
author: rothja
ms.author: jroth
ms.openlocfilehash: e30697dd8b751ec3122683a792a242e6faa0fff0
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91720847"
---
# <a name="dataspace-object-rds"></a>Objeto DataSpace (RDS)
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
 Cria proxies do lado do cliente para objetos comerciais personalizados localizados na camada intermediária.  
  
 O serviço de dados remoto precisa de proxies de objeto de negócios para que os componentes do lado do cliente possam se comunicar com objetos comerciais localizados na camada intermediária. Os proxies facilitam o empacotamento, o empacotamento e o transporte (marshaling) dos dados do [conjunto de registros](../ado-api/recordset-object-ado.md) do aplicativo entre os limites do processo ou da máquina.  
  
 O serviço de dados remotos usa o **RDS. ** Método [CreateObject](./createobject-method-rds.md) do objeto DataSpace para criar proxies de objeto comercial. O proxy de objeto comercial é criado dinamicamente sempre que uma instância de seu equivalente de objeto comercial de camada intermediária é criada. O serviço de dados remoto oferece suporte aos seguintes protocolos: HTTP, HTTPS (soquetes de segurança HTTP), DCOM e em processo (os componentes cliente e o objeto comercial residem no mesmo computador).  
  
> [!NOTE]
>  O RDS se comporta de maneira "sem estado" quando o **RDS. O objeto DataSpace** usa os protocolos http ou HTTPS. Ou seja, todas as informações internas sobre uma solicitação do cliente são descartadas depois que o servidor retorna uma resposta.  
  
> [!NOTE]
>  Embora o objeto comercial pareça existir durante o tempo de vida do proxy de objeto comercial, o objeto comercial realmente existe somente até que uma resposta seja enviada a uma solicitação. Quando uma solicitação é emitida (ou seja, um método é invocado no objeto comercial), o proxy abre uma nova conexão com o servidor e o servidor cria uma nova instância do objeto comercial. Depois que o objeto comercial responde à solicitação, o servidor destrói o objeto comercial e fecha a conexão.  
  
> [!NOTE]
>  Esse comportamento significa que você não pode passar dados de uma solicitação para outra usando uma variável ou propriedade de objeto comercial. Você deve empregar algum outro mecanismo, como um arquivo ou um argumento de método, para manter os dados de estado.  
  
 A ID de classe para o **RDS. O objeto DataSpace** é BD96C556-65A3-11D0-983A-00C04FC29E36.  
  
 O objeto **DataSpace** é seguro para scripts.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto DataSpace (RDS)](./dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método CreateObject e objeto DataSpace (VBScript)](./dataspace-object-and-createobject-method-example-vbscript.md)