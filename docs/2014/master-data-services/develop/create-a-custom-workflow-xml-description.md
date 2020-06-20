---
title: Descrição XML do fluxo de trabalho personalizado (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7cceedac33c3f368f99fd87ab3aa2453f1cf9ba9
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971506"
---
# <a name="custom-workflow-xml-description-master-data-services"></a>Descrição XML do fluxo de trabalho personalizado (Master Data Services)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], o método <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> é chamado pelo serviço de Integração de Fluxo de Trabalho MDS do SQL Server quando um fluxo de trabalho é iniciado. Este método recebe metadados e dados sobre o item que disparou a regra de negócio do fluxo de trabalho como um bloco de XML. Para obter o código de exemplo que implementa um manipulador de fluxo de trabalho, consulte [Exemplo de fluxo de trabalho personalizado&#40;Master Data Services&#41;](create-a-custom-workflow-example.md).  
  
 O seguinte exemplo mostra como deve ser a aparência do XML enviado ao manipulador de fluxo de trabalho:  
  
```scr  
<ExternalAction>  
  <Type>TEST</Type>  
  <SendData>1</SendData>  
  <Server_URL>This is my test!</Server_URL>  
  <Action_ID>Test Workflow</Action_ID>  
  <Model_ID>5</Model_ID>  
  <Model_Name>Customer</Model_Name>  
  <Entity_ID>34</Entity_ID>  
  <Entity_Name>Customer</Entity_Name>  
  <Version_ID>8</Version_ID>  
  <MemberType_ID>1</MemberType_ID>  
  <Member_ID>12</Member_ID>  
  <MemberData>  
    <ID>12</ID>  
    <Version_ID>8</Version_ID>  
    <ValidationStatus_ID>3</ValidationStatus_ID>  
    <ChangeTrackingMask>0</ChangeTrackingMask>  
    <EnterDTM>2011-02-25T20:16:36.650</EnterDTM>  
    <EnterUserID>2</EnterUserID>  
    <EnterUserName>MyUserName</EnterUserName>  
    <EnterUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</EnterUserMuid>  
    <EnterVersionId>8</EnterVersionId>  
    <EnterVersionName>VERSION_1</EnterVersionName>  
    <EnterVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</EnterVersionMuid>  
    <LastChgDTM>2011-02-25T20:16:36.650</LastChgDTM>  
    <LastChgUserID>2</LastChgUserID>  
    <LastChgUserName>MyUserName</LastChgUserName>  
    <LastChgUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</LastChgUserMuid>  
    <LastChgVersionId>8</LastChgVersionId>  
    <LastChgVersionName>VERSION_1</LastChgVersionName>  
    <LastChgVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</LastChgVersionMuid>  
    <Name>Test Customer</Name>  
    <Code>TC</Code>  
  </MemberData>  
</ExternalAction>  
```  
  
 A tabela a seguir descreve algumas das marcas contidas neste XML.  
  
|Marca|Descrição|  
|---------|-----------------|  
|\<Type>|O texto que você inseriu na caixa de texto **Tipo de fluxo de trabalho** no [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] para identificar qual assembly de fluxo de trabalho personalizado deve ser carregado.|  
|\<SendData>|Um valor booliano controlado pela caixa de seleção **Incluir dados de membro na mensagem** no [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Um valor de 1 significa que a \<MemberData> seção é enviada; caso contrário, a \<MemberData> seção não é enviada.|  
|<Server_URL>|O texto que você inseriu na caixa de texto **Site de fluxo de trabalho** no [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
|<Action_ID>|O texto que você inseriu na caixa de texto **Nome do fluxo de trabalho** no [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
|\<MemberData>|Contém os dados do membro que disparou a ação do fluxo de trabalho. Isso só será incluído se o valor de \<SendData> for 1.|  
|\<Enter*xxx*>|Esse conjunto de marcas contém metadados sobre a criação do membro, por exemplo, quando foi criado e quem o criou.|  
|\<LastChg*xxx*>|Esse conjunto de marcas contém metadados sobre as últimas alterações feitas no membro, por exemplo, quando a alteração foi feita e quem a fez.|  
|\<Name>|O primeiro atributo do membro que foi alterado. Este membro de exemplo contém apenas os atributos Name e Code.|  
|\<Code>|O próximo atributo do membro que foi alterado. Se esse membro de exemplo tinha mais atributos, eles viriam depois deste.|  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um &#40;de fluxo de trabalho personalizado Master Data Services&#41;](create-a-custom-workflow-master-data-services.md)   
 [Exemplo de fluxo de trabalho personalizado &#40;Master Data Services&#41;](create-a-custom-workflow-example.md)  
  
  
