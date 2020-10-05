---
description: Propriedade Handler (RDS)
title: Propriedade do manipulador (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
author: rothja
ms.author: jroth
ms.openlocfilehash: 5dc5a8cfc455d27a2bb17b40585e3e38cdd581cf
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722045"
---
# <a name="handler-property-rds"></a>Propriedade Handler (RDS)
Indica o nome de um programa de personalização do lado do servidor (manipulador) que estende a funcionalidade do [RDSServer. datafactory](./datafactory-object-rdsserver.md)e quaisquer parâmetros usados pelo *manipulador*.  
  
 **Aplica-se a:** [objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. Objeto DataControl](./datacontrol-object-rds.md) .  
  
 *Cadeia de caracteres*  
 Um valor de **cadeia de caracteres** que contém o nome do manipulador e quaisquer parâmetros, todos separados por vírgulas (por exemplo, `"handlerName,parm1,parm2,...,parm` *N* `"` ).  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade dá suporte à [personalização](../../guide/remote-data-service/datafactory-customization.md), uma funcionalidade que requer a definição da propriedade [CursorLocation](../ado-api/cursorlocation-property-ado.md) como **adUseClient**.  
  
 O nome do manipulador e seus parâmetros, se houver, são separados por vírgulas (","). O comportamento imprevisível ocorrerá se um ponto-e-vírgula (";") aparecer em qualquer lugar dentro da *cadeia de caracteres*. Você pode escrever seu próprio manipulador, desde que ele dê suporte à interface **IDataFactoryHandler** .  
  
 O nome do manipulador padrão é **MSDFMAP. E seu**parâmetro padrão é um arquivo de personalização chamado **MSDFMAP.INI**. Use essa propriedade para invocar arquivos de personalização alternativos criados pelo administrador do servidor.  
  
 A alternativa para definir a propriedade do **manipulador** é especificar um manipulador e parâmetros na propriedade [ConnectionString](../ado-api/connectionstring-property-ado.md) ; ou seja, "**Handler =**_handlename, parâmetro1, parâmetro2,...;_".  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Handler (VB)](./handler-property-example-vb.md)   
 [Personalização de datafactory](../../guide/remote-data-service/datafactory-customization.md)   
 [Objeto DataFactory (RDSServer)](./datafactory-object-rdsserver.md)