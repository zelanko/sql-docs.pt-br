---
title: Coleta de dados no controle ReportViewer 2016 | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: application-integration
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
caps.latest.revision: 2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5d41ac350e03dfbecc53041b2bbfa2570ede717c
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926847"
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>Integrando o Reporting Services usando os controles ReportViewer – coleta de dados
Por padrão, o controle ReportViewer coleta informações de uso anônimas para que a Microsoft entenda melhor como os clientes estão fazendo uso do controle. Ao criar uma melhor compreensão de como os clientes estão implantando e usando o Controle do Visualizador, o desenvolvimento futuro pode se concentrar em melhorias que entregam o maior valor aos clientes.

Para ver uma explicação sobre as práticas de coleta e de uso de dados do usuário das versões do Microsoft SQL Server 2016 e de outros produtos e serviços, confira esta [política de privacidade]((http://go.microsoft.com/fwlink/?LinkID=868444)).

## <a name="opting-out-of-telemetry"></a>Recusando a telemetria

A telemetria pode ser desabilitada de forma programática por meio de “EnableTelemetry”. Faça isso editando a página .aspx que hospeda o controle

```
\<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
\</rsweb:ReportViewer>
```

Ou de forma prática antes que o controle seja renderizado, como em chamada de Page_Load da página de hospedagem.
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>Confira também

[Usando o controle WebForms ReportViewer](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[Integrando o Reporting Services usando os controles ReportViewer](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



