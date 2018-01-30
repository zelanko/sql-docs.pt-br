---
title: "Atualizar pastas de trabalho e atualização de dados agendada (SharePoint 2013) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a49c4af4-e243-4926-be97-74da1f9d54eb
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b76561da72c6a4502f451d9ee39f8e9f90c97546
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2018
---
# <a name="upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013"></a>Atualizar pastas de trabalho e atualização de dados agendada (SharePoint 2013)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Este tópico explica a experiência do usuário das pastas de trabalho criadas no anterior [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] ambientes e como atualizar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] pastas de trabalho para que você pode tirar proveito dos novos recursos introduzidos nesta versão. Para saber mais sobre os novos recursos, veja [Novidades no Power Pivot](http://go.microsoft.com/fwlink/?LinkID=203917).  
  
> [!WARNING]  
>  Você não pode reverter uma atualização para pastas de trabalho que são atualizadas automaticamente no servidor. Quando uma pasta de trabalho é atualizada, ela permanece atualizada. Para usar uma versão anterior, você pode republicar a pasta de trabalho anterior para o SharePoint, restaurar uma versão anterior ou reciclar a pasta de trabalho. Para obter mais informações sobre como restaurar ou reciclar um documento no SharePoint, consulte [Planejar para proteger o conteúdo usando lixeiras e controle de versão](http://go.microsoft.com/fwlink/?LinkId=238669).  
  
  
##  <a name="bkmk_overview"></a> Visão geral de como atualizar pastas de trabalho  
 Uma pasta de trabalho do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] é uma pasta de trabalho do Excel que contém dados inseridos do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Atualizar uma pasta de trabalho tem dois benefícios:  
  
-   Usar novos recursos no [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)].  
  
-   Habilita a atualização de dados agendada para pastas de trabalho que são executadas com um servidor do Analysis Services do [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] no modo do SharePoint.  
  
> [!IMPORTANT]  
>  Você não pode reverter uma pasta de trabalho atualizada, portanto, faça uma cópia do arquivo se desejar usá-lo na versão anterior do [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)], ou em uma versão anterior do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 A tabela a seguir lista o suporte e o comportamento de pastas de trabalho do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] com base no ambiente no qual a pasta de trabalho foi criada. O comportamento descrito inclui a experiência geral do usuário, as opções de atualização com suporte para atualizar a pasta de trabalho para o ambiente específico e o comportamento da atualização de dados agendada de uma pasta de trabalho que ainda não foi atualizada.  
  
### <a name="workbook-behavior-and-upgrade-options"></a>Comportamento da pasta de trabalho e opções de atualização  
  
|Criado em|\<|Suporte e comportamento|>|  
|----------------|--------|--------------------------|--------|  
||**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2010**|**2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2010**|**2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013**|  
|**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010**|Todos os recursos|**Experiência:** os usuários podem interagir com a pasta de trabalho no navegador e usá-la como uma fonte de dados para outras soluções.<br /><br /> **Atualização:** as pastas de trabalho serão atualizadas automaticamente na biblioteca de documentos se a Atualização Automática estiver habilitada para o serviço do sistema do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no farm do SharePoint.<br /><br /> **Atualização de dados agendada:** SEM suporte. A pasta de trabalho precisa ser atualizada.|**Experiência:** os usuários podem interagir com a pasta de trabalho e usá-la como uma fonte de dados para outras soluções.<br /><br /> **Atualização:** a atualização automática não está disponível. Os usuários devem atualizar manualmente suas pastas de trabalho do 2008 R2 para a versão 2012 ou para a versão 2013 do Office.<br /><br /> **Atualização de dados agendada:** SEM suporte. A pasta de trabalho precisa ser atualizada.|  
|**2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel**|Sem suporte|Todos os recursos|**Experiência:** os usuários podem interagir com a pasta de trabalho no navegador e usá-la como uma fonte de dados para outras soluções. A atualização de dados agendada está disponível.<br /><br /> **Atualização:** a atualização automática não tem suporte. Os usuários podem atualizar manualmente suas pastas de trabalho para a versão 2013 do Office.<br /><br /> **Atualização de dados agendada:** com suporte.|  
|**Excel 2013**|Sem suporte|Sem suporte|Todos os recursos|  
  
##  <a name="bkmk_to_2012sp1_from_2008r2"></a> Atualizar para pastas de trabalho do SQL Server 2012 Service Pack 1 (SP1) de pastas de trabalho do 2008 R2  
 Esta seção descreve como atualizar para pastas de trabalho do SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2013 de pastas de trabalho do SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010.  
  
 **Alteração de comportamento:** as pastas de trabalho do SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] não serão atualizadas automaticamente quando são usadas no SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013. Portanto, as atualizações de dados agendadas não funcionarão para pastas de trabalho do SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]  
  
 As pastas de trabalho do 2008 R2 serão abertas no [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013, porém as atualizações de dados agendadas não funcionarão. Se você revisar o histórico de atualização, verá uma mensagem de erro semelhante à seguinte:  
  
 “A pasta de trabalho contém um modelo do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] sem suporte. O modelo do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] na pasta de trabalho está no formato do SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010. Os modelos do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] com suporte são os seguintes:  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010.  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2013.  
  
 **Como atualizar uma pasta de trabalho:** a atualização de dados agendada não funcionará até você atualizar para uma pasta de trabalho do 2012. Para atualizar a pasta de trabalho e o modelos que ela contém, siga um destes procedimentos:  
  
-   Baixe e abra a pasta de trabalho no Microsoft Excel 2010 com o suplemento SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel instalado.  
  
     Abra a janela do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e atualize o modelo do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     Salve a pasta de trabalho e republique-a no SharePoint.  
  
-   Baixe e abra a pasta de trabalho no Microsoft Excel 2013.  
  
     Abra a janela do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e atualize o modelo do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     Salve a pasta de trabalho e republique-a no servidor do SharePoint.  
  
 Para obter mais informações sobre as alterações em recursos do Analysis Services, veja [Alterações no comportamento de recursos do Analysis Services no SQL Server 2016](../../../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)  
  
 Para obter mais informações sobre o histórico de atualizações, veja [Exibir o histórico de atualizações de dados &#40;Power Pivot para SharePoint&#41;](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_to_2012sp1_from_2012"></a> Atualizar, partindo de versões criadas usando o suplemento Power Pivot 2012 para Excel, para pastas de trabalho do Office 2013  
 Esta seção descreve como atualizar **para** o SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no Excel 2013 **de** pastas de trabalho do SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010.  
  
 Atualizar uma pasta de trabalho resolve o seguinte erro que ocorre ao tentar atualizar dados agendados na versão anterior da pasta de trabalho:  
  
 “A operação de atualização de pastas de trabalho criadas com a versão anterior do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] não está disponível.”  
  
 **Como atualizar uma pasta de trabalho**  
  
1.  Atualizar cada pasta de trabalho manualmente abrindo-a no Microsoft Excel 2013.  
  
2.  Para atualizar a pasta de trabalho e o modelo que ela contém, baixe e abra a pasta de trabalho no Microsoft Excel 2013.  
  
3.  Abra a janela do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e atualize o modelo do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
4.  Salve a pasta de trabalho e republique-a no servidor do SharePoint 2013.  
  
##  <a name="bkmk_to_2012_from_2008R2"></a> Atualizar para pastas de trabalho do SQL Server 2012 de versões criadas usando o suplemento Power Pivot 2008 R2 para Excel 2010  
 Esta seção descreve como atualizar **para** o SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010 **de** pastas de trabalho do SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010.  
  
 Atualizar uma pasta de trabalho resolve o seguinte erro que ocorre ao tentar atualizar dados agendados na versão anterior da pasta de trabalho:  
  
 “A operação de atualização de pastas de trabalho criadas com a versão anterior do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] não está disponível.”  
  
 **Como atualizar uma pasta de trabalho**  
  
 A atualização pode ser feita de duas maneiras:  
  
1.  Atualize cada pasta de trabalho manualmente abrindo-a no Excel em um computador que tem a versão [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel e republicá-la no servidor. Quando a pasta de trabalho é aberta na versão mais recente do suplemento, ocorrem as seguintes operações internas: o provedor de dados na cadeia de conexão de dados da pasta de trabalho é atualizado para o MSOLAP.5; os metadados são atualizados e as relações são recriadas para se conformarem à implementação mais recente.  
  
2.  Como alternativa, um administrador do SharePoint pode habilitar o recurso da atualização automática para o Serviço do Sistema [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] em um farm do SharePoint para atualizar automaticamente uma pasta de trabalho do [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)][!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] quando a atualização de dados agendada for executada (são atualizadas somente pastas de trabalho que são configuradas para atualização de dados agendada).  
  
    > [!NOTE]  
    >  Atualização automática é um recurso de configuração de servidor; você não pode habilitá-lo nem desabilitá-lo para pastas de trabalho, bibliotecas ou coleções de sites específicas.  
  
 **Como configurar a atualização automática durante a atualização de dados**  
  
 Para usar a atualização automática, é necessário marcar a caixa de seleção **Atualizar automaticamente as pastas de trabalho do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para habilitar a atualização de dados do servidor** na Ferramenta de Configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]. Na ferramenta, a caixa de seleção estará na página **Atualizar Serviço de Sistema do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]** e também na página **Criar Aplicativo de Serviço [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]** se você estiver configurando uma nova instalação.  
  
 Você pode executar o cmdlet a seguir para verificar se a atualização automática está habilitada:  
  
```  
PS C:\Windows\system32> Get-PowerPivotSystemService  
```  
  
 A saída de Obtém-PowerPivotSystemService é uma lista de propriedades e valores correspondentes. **WorkbookUpgradeOnDataRefresh** deve ser exibido na lista de propriedades. Será definido como **true** se a atualização automática estiver habilitada. Se for **false**, continue na próxima etapa, habilitando a atualização automática da pasta de trabalho.  
  
 Para habilitar a atualização automática da pasta de trabalho, execute o seguinte comando:  
  
```  
PS C:\Windows\system32> Set-PowerPivotSystemService –WorkbookUpgradeOnDataRefresh:$true –Confirm:$false  
```  
  
 Depois de atualizar a pasta de trabalho, poderá usar a atualização de dados agendada e novos recursos no suplemento [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel.  
  
##  <a name="bkmk_runold"></a> Executando várias versões de pasta de trabalho em um servidor mais recente  
 Você pode executar versões mais antigas e mais novas de pastas de trabalho [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] lado a lado em uma instância do [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 Dependendo de como você instalou o servidor, **poderá ser necessário** instalar uma versão anterior do provedor OLE DB do Analysis Services antes que seja possível acessar pastas de trabalho mais antigas e mais novas no mesmo servidor.  
  
 Observe que a publicação de pastas de trabalho de versões mais novas em instâncias do SQL Server do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] não tem suporte. Uma instância do [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] não carregará uma pasta de trabalho que você criou na versão do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] do [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)], e uma instância do SQL Server 2012 não carregará pastas de trabalho do Office 2013 com modelos de dados avançados que você criou usando a versão do [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel.  
  
###  <a name="bkmk_msolapxslx"></a> Como verificar informações do provedor de dados MSOLAP em uma pasta de trabalho do Power Pivot  
 Use as instruções a seguir para verificar qual provedor OLE DB é usado em uma pasta de trabalho do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . A verificação das informações de conexão de dados não exige a instalação do suplemento [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] .  
  
1.  No Excel, na guia Dados, clique em **Conexões**. Clique em **Propriedades**.  
  
2.  Na guia **Definição** , a versão do provedor é exibida no início da cadeia de conexão.  
  
     **Provider=MSOLAP.5** indica que a pasta de trabalho é [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
     **Provider=MSOLAP.4** indica [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)].  
  
     **Data Source=$Embedded$** indica que a pasta de trabalho é uma pasta de trabalho do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , usando um banco de dados inserido.  
  
###  <a name="bkmk_msolappc"></a> Como verificar a versão atual do provedor de dados MSOLAP em um computador local  
 Use as instruções a seguir para verificar qual provedor OLE DB é a versão atual no servidor ou estação de trabalho que executa pastas de trabalho do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Saber a versão atual pode ajudar a solucionar problemas relacionados a erros de conexão de dados após a atualização.  
  
1.  No Editor do Registro, vá para HKEY_CLASSES_ROOT  
  
2.  Role até MSOLAP. Verifique se MSOLAP.5 está listado entre os provedores OLAP instalados no sistema. Verifique se MSOLAP|CurVer está definido como MSOLAP.5  
  
## <a name="see-also"></a>Consulte também  
 [Migrar o Power Pivot para o SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [Atualizar Power Pivot para SharePoint](../../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Novidades do Analysis Services](../../../analysis-services/what-s-new-in-analysis-services.md)   
 [Atualização de dados de exibição histórico &#40; PowerPivot para SharePoint &#41;](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
  
