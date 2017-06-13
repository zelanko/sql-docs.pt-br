---
title: "Acessar itens do servidor de relatório com acesso à URL | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- referencing URL items for report server access
- URL access [Reporting Services], report servers
ms.assetid: a58b4ca6-129d-45e9-95c7-e9169fe5bba4
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b05886a719709061a7d2e5d98b1d5560d24dc839
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="access-report-server-items-using-url-access"></a>Acessar itens do Servidor de Relatório usando o acesso à URL
  Este tópico descreve como acessar itens de catálogo de tipos diferentes em um banco de dados de servidor de relatório ou em um site do SharePoint usando*rs:Command*=*Value*. Não é necessário adicionar de fato essa cadeia de caracteres de parâmetro. Se você omiti-la, o servidor de relatório avaliará o tipo de item e selecionará o valor de parâmetro apropriado automaticamente. No entanto, usar a cadeia de caracteres *rs:Command*=*Value* na URL melhora o desempenho do servidor de relatórios.  
  
 Observe a sintaxe do proxy `_vti_bin` nos exemplos a seguir. Para obter mais informações sobre como usar a sintaxe do proxy, consulte [Referência de parâmetro de acesso à URL](../reporting-services/url-access-parameter-reference.md).  
  
## <a name="access-a-report"></a>Acessar um relatório  
 Para exibir um relatório no navegador, use o parâmetro *rs:Command*=*Render* . Por exemplo:  
  
 **Nativo** `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`  
  
> [!TIP]  
>  É importante que a URL inclua a sintaxe do proxy `_vti_bin` para rotear a solicitação através do SharePoint e do proxy HTTP [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . O proxy adiciona qualquer contexto à solicitação HTTP, o contexto necessário para garantir a execução adequada do relatório para servidores de relatório no modo do SharePoint.  
  
## <a name="access-a-resource"></a>Acessar um recurso  
 Para acessar um recurso, use o parâmetro *rs:Command*=*GetResourceContents* . Se o recurso for compatível com o navegador, como uma imagem, ele será aberto no navegador. Caso contrário, você será solicitado a abrir ou salvar o arquivo ou recurso em disco.  
  
 **Nativo** `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`  
  
## <a name="access-a-data-source"></a>Acessar uma fonte de dados  
 Para acessar uma fonte de dados, use o parâmetro *rs:Command*=*GetDataSourceContents* . Se houver suporte para XML, a definição da fonte de dados será exibida se você for um usuário autenticado com a permissão **Ler Conteúdo** na fonte de dados. Por exemplo:  
  
 **Nativo** `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 A estrutura XML pode ter uma aparência semelhante a esta:  
  
```  
<DataSourceDefinition>  
   <Extension>SQL</Extension>  
   <ConnectString>Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security Info=False;Initial Catalog=AdventureWorks2012;Data Source=MYSERVER1;</ConnectString>  
   <CredentialRetrieval>Integrated</CredentialRetrieval>  
   <WindowsCredentials>False</WindowsCredentials>  
   <ImpersonateUser>False</ImpersonateUser>  
   <Prompt />  
   <Enabled>True</Enabled>  
</DataSourceDefinition>  
```  
  
 A cadeia de conexão é retornada com base na configuração **SecureConnectionLevel** do servidor de relatório. Para obter mais informações sobre a configuração **SecureConnectionLevel** , consulte [Usando métodos seguros do serviço Web](../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md).  
  
## <a name="access-the-contents-of-a-folder"></a>Acessar o conteúdo de uma pasta  
 Para acessar o conteúdo de uma pasta, use o parâmetro *rs:Command*=*GetChildren* . Uma página genérica de navegação em pasta será retornada contendo links para subpastas, relatórios, fontes de dados e recursos na pasta solicitada. Por exemplo:  
  
 **Nativo** `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rs:Command=GetChildren`  
  
 A interface do usuário que você vê é semelhante ao modo de procura do diretório usado pelo [!INCLUDE[msCoName](../includes/msconame-md.md)] IIS (Servidor de Informações da Internet). O número de versão, inclusive o número de compilação, do servidor de relatório também é exibido embaixo da listagem de pastas.  
  
## <a name="see-also"></a>Consulte também  
 [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](../reporting-services/url-access-parameter-reference.md)  
  
  
