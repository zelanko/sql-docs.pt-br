---
title: Coleta de dados 2016 do controle ReportViewer | Microsoft Docs
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
caps.latest.revision: 2
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4e8b0226c27380bd2089acf8d2d6c8d7b27c7c5b
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>Integrando o Reporting Services usando os controles ReportViewer - coleta de dados
Por padrão, o controle ReportViewer coleta informações de uso anônimas em ordem para a Microsoft entender melhor como os clientes estão fazendo uso do controle. Criando uma melhor compreensão de como os clientes estão implantando e usando o controle do visualizador, desenvolvimento futuro pode se concentrar em melhorias que fornecem o maior valor aos clientes.

Para ver uma explicação sobre as práticas de coleta e de uso de dados do usuário das versões do Microsoft SQL Server 2016 e de outros produtos e serviços, consulte esta [política de privacidade da Microsoft](https://www.microsoft.com/EN-US/privacystatement/SQLServer/Default.aspx).

## <a name="opting-out-of-telemetry"></a>Recusando a Telemetria

Telemetria pode ser desabilitada programaticamente por meio de "EnableTelemetry". Isso pode ser feito editando a página. aspx hospedando o controle

```
\<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
\</rsweb:ReportViewer>
```

Ou então, pragmatically antes que o controle é processado, como em chamada de Page_Load da página de hospedagem.
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>Consulte também

[Usando o controle ReportViewer do WebForms](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[Integrando o Reporting Services usando os controles ReportViewer](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 




