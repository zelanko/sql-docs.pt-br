---
title: Coleta de dados no Controle do ReportViewer
description: Dados de uso anônimos são coletados pelo controle para entender melhor como os clientes usam o produto. Os dados de uso permitem que o desenvolvimento futuro se concentre nos aprimoramentos que são mais relevantes para os clientes.
author: maggiesMSFT
ms.author: maggies
ms.custom: ''
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.date: 09/18/2018
ms.openlocfilehash: d7b70445fc4d8a29d8ebcdf7ecbffe4b54133f0e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74796889"
---
# <a name="integrate-reporting-services-using-reportviewer-controls---data-collection"></a>Integrar o Reporting Services usando os controles ReportViewer – coleta de dados

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



