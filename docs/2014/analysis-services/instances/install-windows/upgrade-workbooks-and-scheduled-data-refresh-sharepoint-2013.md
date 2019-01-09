---
title: Atualizar pastas de trabalho e atualização de dados agendada (SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: a49c4af4-e243-4926-be97-74da1f9d54eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3ed3fc8546ef7bd85934d8b127ff124acc095e29
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53373931"
---
# <a name="upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013"></a>Atualizar pastas de trabalho e atualização de dados agendada (SharePoint 2013)
  Este tópico explica a experiência do usuário das pastas de trabalho criadas em ambientes anteriores do PowerPivot e como atualizar pastas de trabalho PowerPivot de forma que você possa aproveitar os novos recursos introduzidos nesta versão. Para saber mais sobre os novos recursos, consulte [Novidades no PowerPivot](https://go.microsoft.com/fwlink/?LinkID=203917).  
  
> [!WARNING]  
>  Você não pode reverter uma atualização para pastas de trabalho que são atualizadas automaticamente no servidor. Quando uma pasta de trabalho é atualizada, ela permanece atualizada. Para usar uma versão anterior, você pode republicar a pasta de trabalho anterior para o SharePoint, restaurar uma versão anterior ou reciclar a pasta de trabalho. Para obter mais informações sobre como restaurar ou reciclar um documento no SharePoint, consulte [Planejar para proteger o conteúdo usando lixeiras e controle de versão](https://go.microsoft.com/fwlink/?LinkId=238669).  
  
 Este tópico contém as seguintes seções:  
  
-   [Visão geral de como atualizar pastas de trabalho](#bkmk_overview)  
  
-   [Atualizar para pastas de trabalho do SQL Server 2012 Service Pack 1 (SP1) de pastas de trabalho do 2008 R2](#bkmk_to_2012sp1_from_2008r2)  
  
-   [Atualizar para pastas de trabalho do Office 2013 de versões criadas usando o 2012 Add-In PowerPivot para Excel](#bkmk_to_2012sp1_from_2012)  
  
-   [Atualizar para pastas de trabalho do SQL Server 2012 de versões criadas usando o 2008 R2 PowerPivot Add-In para o Excel 2010](#bkmk_to_2012_from_2008R2)  
  
-   [Executando várias versões de pasta de trabalho em um servidor mais recente](#bkmk_runold)  
  
##  <a name="bkmk_overview"></a> Visão geral de como atualizar pastas de trabalho  
 Uma pasta de trabalho PowerPivot é uma pasta de trabalho do Excel que contém dados PowerPivot inseridos. Atualizar uma pasta de trabalho tem dois benefícios:  
  
-   Usar novos recursos no [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)].  
  
-   Habilita a atualização de dados agendada para pastas de trabalho que são executadas com um servidor do Analysis Services do [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] no modo do SharePoint.  
  
> [!IMPORTANT]  
>  Você não pode reverter uma pasta de trabalho atualizada, portanto, faça uma cópia do arquivo se desejar usá-lo na versão anterior do [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)], ou em uma versão anterior do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 A tabela a seguir lista o suporte e o comportamento de pastas de trabalho PowerPivot com base no ambiente no qual a pasta de trabalho foi criada. O comportamento descrito inclui a experiência geral do usuário, as opções de atualização com suporte para atualizar a pasta de trabalho para o ambiente específico e o comportamento da atualização de dados agendada de uma pasta de trabalho que ainda não foi atualizada.  
  
### <a name="workbook-behavior-and-upgrade-options"></a>Comportamento da pasta de trabalho e opções de atualização  
  
|Criado em|\<|Suporte e comportamento|>|  
|----------------|--------|--------------------------|--------|  
||**2008 R2 PowerPivot para SharePoint 2010**|**2012 PowerPivot para SharePoint 2010**|**2012 SP1 PowerPivot para SharePoint 2013**|  
|**2008 R2 PowerPivot para Excel 2010**|Todos os recursos|**Experiência:** Os usuários podem interagir com a pasta de trabalho no navegador e usá-la como uma fonte de dados para outras soluções.<br /><br /> **Atualização:** As pastas de trabalho serão atualizadas automaticamente na biblioteca de documentos se a Atualização Automática estiver habilitada para o serviço do sistema do PowerPivot no farm do SharePoint.<br /><br /> **Agendar atualização de dados:** SEM suporte. A pasta de trabalho precisa ser atualizada.|**Experiência:** Os usuários podem interagir com a pasta de trabalho e usá-la como uma fonte de dados para outras soluções.<br /><br /> **Atualização:** A atualização automática não está disponível. Os usuários devem atualizar manualmente suas pastas de trabalho do 2008 R2 para a versão 2012 ou para a versão 2013 do Office.<br /><br /> **Agendar atualização de dados:** SEM suporte. A pasta de trabalho precisa ser atualizada.|  
|**2012 PowerPivot para Excel**|Sem suporte|Todos os recursos|**Experiência:** Os usuários podem interagir com a pasta de trabalho no navegador e usá-la como uma fonte de dados para outras soluções. A atualização de dados agendada está disponível.<br /><br /> **Atualização:** A atualização automática não tem suporte. Os usuários podem atualizar manualmente suas pastas de trabalho para a versão 2013 do Office.<br /><br /> **Atualização de dados agendada:** com suporte.|  
|**Excel 2013**|Sem suporte|Sem suporte|Todos os recursos|  
  
##  <a name="bkmk_to_2012sp1_from_2008r2"></a> Atualizar para pastas de trabalho do SQL Server 2012 Service Pack 1 (SP1) de pastas de trabalho do 2008 R2  
 Esta seção descreve como atualizar para pastas de trabalho do SQL Server 2012 SP1 PowerPivot para Excel 2013 de pastas de trabalho do SQL Server 2008 R2 PowerPivot para Excel 2010.  
  
 **Alteração de comportamento:** As pastas de trabalho do SQL Server 2008 R2 PowerPivot não serão atualizadas automaticamente quando são usadas no SQL Server 2012 SP1 PowerPivot para SharePoint 2013. Portanto, as atualizações de dados agendadas não funcionarão para pastas de trabalho do SQL Server 2008 R2 PowerPivot  
  
 As pastas de trabalho do 2008 R2 serão abertas no PowerPivot para SharePoint 2013, porém as atualizações de dados agendadas não funcionarão. Se você revisar o histórico de atualização, verá uma mensagem de erro semelhante à seguinte:  
  
 "A pasta de trabalho contém um modelo PowerPivot sem suporte. O modelo do PowerPivot na pasta de trabalho está no formato do SQL Server 2008 R2 PowerPivot para Excel 2010. Os modelos do PowerPivot com suporte são os seguintes:  
  
-   SQL Server 2012 PowerPivot para Excel 2010.  
  
-   SQL Server 2012 PowerPivot para Excel 2013.  
  
 **Como atualizar uma pasta de trabalho:** A atualização de dados agendada não funcionará até você atualizar para uma pasta de trabalho do 2012. Para atualizar a pasta de trabalho e o modelos que ela contém, siga um destes procedimentos:  
  
-   Baixe e abra a pasta de trabalho no Microsoft Excel 2010 com o suplemento SQL Server 2012 PowerPivot para Excel instalado.  
  
     Abra a janela do PowerPivot e atualize o modelo do PowerPivot.  
  
     Salve a pasta de trabalho e republique-a no SharePoint.  
  
-   Baixe e abra a pasta de trabalho no Microsoft Excel 2013.  
  
     Abra a janela do PowerPivot e atualize o modelo do PowerPivot.  
  
     Salve a pasta de trabalho e republique-a no servidor do SharePoint.  
  
 Para obter mais informações sobre alterações em recursos do Analysis Services, consulte [alterações de comportamento para recursos do Analysis Services no SQL Server 2014](../../behavior-changes-to-analysis-services-features-in-sql-server-2014.md)  
  
 Para obter mais informações sobre o histórico de atualização, consulte [histórico de atualização de dados de exibição &#40;PowerPivot para SharePoint&#41;](../../power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_to_2012sp1_from_2012"></a> Atualizar para pastas de trabalho do Office 2013 de versões criadas usando o 2012 Add-In PowerPivot para Excel  
 Essa seção descreve como atualizar **para** o SQL Server 2012 SP1 PowerPivot no Excel 2013 **de** pastas de trabalho do SQL Server 2012 PowerPivot para Excel 2010.  
  
 Atualizar uma pasta de trabalho resolve o seguinte erro que ocorre ao tentar atualizar dados agendados na versão anterior da pasta de trabalho:  
  
 "A operação de atualização para pastas de trabalho criadas com a versão anterior do PowerPivot não está disponível."  
  
 **Como atualizar uma pasta de trabalho**  
  
1.  Atualizar cada pasta de trabalho manualmente abrindo-a no Microsoft Excel 2013.  
  
2.  Para atualizar a pasta de trabalho e o modelo que ela contém, baixe e abra a pasta de trabalho no Microsoft Excel 2013.  
  
3.  Abra a janela do PowerPivot e atualize o modelo do PowerPivot.  
  
4.  Salve a pasta de trabalho e republique-a no servidor do SharePoint 2013.  
  
##  <a name="bkmk_to_2012_from_2008R2"></a> Atualizar para pastas de trabalho do SQL Server 2012 de versões criadas usando o 2008 R2 PowerPivot Add-In para o Excel 2010  
 Essa seção descreve como atualizar **para** o SQL Server 2012 PowerPivot para Excel 2010 **de** pastas de trabalho do SQL Server 2008 R2 PowerPivot para Excel 2010.  
  
 Atualizar uma pasta de trabalho resolve o seguinte erro que ocorre ao tentar atualizar dados agendados na versão anterior da pasta de trabalho:  
  
 "A operação de atualização para pastas de trabalho criadas com a versão anterior do PowerPivot não está disponível."  
  
 **Como atualizar uma pasta de trabalho**  
  
 A atualização pode ser feita de duas maneiras:  
  
1.  Atualizar cada pasta de trabalho manualmente abrindo-a no Excel em um computador que tem a versão [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] do PowerPivot para Excel e então republicá-la no servidor. Quando a pasta de trabalho é aberta na versão mais recente do suplemento, ocorrem as seguintes operações internas: o provedor de dados na cadeia de conexão de dados da pasta de trabalho é atualizado para o MSOLAP.5; os metadados são atualizados e as relações são recriadas para se conformarem à implementação mais recente.  
  
2.  Como alternativa, um administrador do SharePoint pode habilitar o recurso da atualização automática para o Serviço do Sistema PowerPivot em um farm do SharePoint para atualizar automaticamente uma pasta de trabalho PowerPivot do [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] quando a atualização de dados agendada for executada (são atualizadas somente pastas de trabalho que são configuradas para atualização de dados agendada).  
  
    > [!NOTE]  
    >  Atualização automática é um recurso de configuração de servidor; você não pode habilitá-lo nem desabilitá-lo para pastas de trabalho, bibliotecas ou coleções de sites específicas.  
  
 **Como configurar a atualização automática durante a atualização de dados**  
  
 Para usar a atualização automática, você deve marcar a caixa de seleção **Atualizar automaticamente as pastas de trabalho PowerPivot para habilitar a atualização de dados do servidor** na Ferramenta de Configuração do PowerPivot. Dentro da ferramenta, a caixa de seleção está na página **Atualizar Serviço de Sistema do PowerPivot** e, na página **Criar Aplicativo de Serviço PowerPivot** se você estiver configurando uma nova instalação.  
  
 Você pode executar o cmdlet a seguir para verificar se a atualização automática está habilitada:  
  
```  
PS C:\Windows\system32> Get-PowerPivotSystemService  
```  
  
 A saída de Obtém-PowerPivotSystemService é uma lista de propriedades e valores correspondentes. Você deve ver `WorkbookUpgradeOnDataRefresh` na lista de propriedades. Será definido como **true** se a atualização automática estiver habilitada. Se for **false**, continue na próxima etapa, habilitando a atualização automática da pasta de trabalho.  
  
 Para habilitar a atualização automática da pasta de trabalho, execute o seguinte comando:  
  
```  
PS C:\Windows\system32> Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true -Confirm:$false  
```  
  
 Depois de atualizar a pasta de trabalho, poderá usar a atualização de dados agendada e novos recursos no suplemento PowerPivot para Excel.  
  
##  <a name="bkmk_runold"></a> Executando várias versões de pasta de trabalho em um servidor mais recente  
 Você pode executar versões mais antigas e mais novas de pastas de trabalho PowerPivot lado a lado em uma instância do [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 Dependendo de como você instalou o servidor, **poderá ser necessário** instalar uma versão anterior do provedor OLE DB do Analysis Services antes que seja possível acessar pastas de trabalho mais antigas e mais novas no mesmo servidor.  
  
 Observe que a publicação de pastas de trabalho de versões mais novas em instâncias do SQL Server do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] não tem suporte. Uma instância do [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] não carregará uma pasta de trabalho que você criou na versão do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] do [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)], e uma instância do SQL Server 2012 não carregará pastas de trabalho do Office 2013 com modelos de dados avançados que você criou usando a versão do [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] do PowerPivot para Excel.  
  
###  <a name="bkmk_msolapxslx"></a> Como verificar informações do provedor de dados MSOLAP em uma pasta de trabalho do PowerPivot  
 Use as instruções a seguir para verificar qual provedor OLE DB é usado em uma pasta de trabalho PowerPivot. A verificação das informações de conexão de dados não exige a instalação do suplemento [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] .  
  
1.  No Excel, na guia Dados, clique em **Conexões**. Clique em **Propriedades**.  
  
2.  Na guia **Definição** , a versão do provedor é exibida no início da cadeia de conexão.  
  
     **Provider=MSOLAP.5** indica que a pasta de trabalho é [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
     **Provider=MSOLAP.4** indica [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)].  
  
     **Fonte de dados = $ $Embedded** indica que a pasta de trabalho é uma pasta de trabalho do PowerPivot, usando um banco de dados inserido.  
  
###  <a name="bkmk_msolappc"></a> Como verificar a versão atual do provedor de dados MSOLAP em um computador local  
 Use as instruções a seguir para verificar qual provedor OLE DB é a versão atual no servidor ou estação de trabalho que executa pastas de trabalho PowerPivot. Saber a versão atual pode ajudar a solucionar problemas relacionados a erros de conexão de dados após a atualização.  
  
1.  No Editor do Registro, vá para HKEY_CLASSES_ROOT  
  
2.  Role até MSOLAP. Verifique se MSOLAP.5 está listado entre os provedores OLAP instalados no sistema. Verifique se MSOLAP|CurVer está definido como MSOLAP.5  
  
## <a name="see-also"></a>Consulte também  
 [Migrar o PowerPivot para SharePoint 2013](migrate-power-pivot-to-sharepoint-2013.md)   
 [Atualizar o PowerPivot para SharePoint](../../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [O que há de novo no Analysis Services e Business Intelligence](../../what-s-new-in-analysis-services.md)   
 [Exibir histórico de atualização de dados &#40;PowerPivot para SharePoint&#41;](../../power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
  
