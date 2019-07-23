---
title: Coleta de dados no Controle do ReportViewer 2016
uthor: markingmyname
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.custom: ''
ms.date: 09/18/2018
ms.openlocfilehash: 747c073907158e16a16dc8acd7f36ec457e32e80
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68256091"
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>Integrando o Reporting Services usando os controles ReportViewer – coleta de dados

Dados de uso anônimos são coletados pelo controle para entender melhor como os clientes usam o produto. Dados de uso permitem que o desenvolvimento futuro se concentre nas melhorias que são mais relevantes para os clientes.

Uma explicação das práticas de uso e coleta de dados do Microsoft SQL Server e do Visualizador de Relatórios está disponível na [política de privacidade](https://go.microsoft.com/fwlink/?LinkID=868444).

## <a name="opting-out-of-data-collection"></a>Recusar a coleta de dados

A coleta de dados de uso pode ser desabilitada por meio da propriedade ```EnableTelemetry```.

```xml
<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
</rsweb:ReportViewer>
```

Ou, de forma pragmática, antes que o controle seja renderizado.
    
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>Confira também

[Usando o controle WebForms do Visualizador de Relatórios](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[Integrando o Reporting Services usando os controles do Visualizador de Relatórios](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



