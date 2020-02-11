---
title: Alterações de comportamento para Analysis Services recursos no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a5525984fa4b1f1823f526097d271780a072bd4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67284806"
---
# <a name="behavior-changes-to-analysis-services-features-in-sql-server-2014"></a>Alterações no comportamento de recursos do Analysis Services no SQL Server 2014
  Este tópico descreve as alterações de comportamento do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para implementações multidimensionais, tabulares, de mineração de dados e [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] . As alterações de comportamento afetam a maneira como os recursos funcionam ou interagem na versão atual em comparação com as versões anteriores do SQL Server.  
  
> [!NOTE]  
>  Em contraste, uma alteração significativa é aquela que impede a execução de um modelo de dados ou aplicativo integrado com [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para obter mais informações, consulte [Breaking Changes to Analysis Services Features in SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md).  
  
 Neste tópico:  
  
-   [Alterações de comportamento no SQL Server 2014](#bkmk_sql2014)  
  
-   [Alterações de comportamento no SQL Server 2012 SP1](#bkmk_sql2012sp1)  
  
-   [Alterações de comportamento no SQL Server 2012](#bkmk_sql2012)  
  
##  <a name="bkmk_sql2014"></a>Alterações de comportamento em[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Nenhuma nova alteração de comportamento anunciada para mineração de dados tabular, multidimensional ou recursos [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] nesta versão.  No entanto, como  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] é tão semelhante às versões [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] , as alterações de comportamento de ambas as versões anteriores são fornecidas aqui como uma conveniência, se você estiver atualizando do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
##  <a name="bkmk_sql2012sp1"></a>Alterações de comportamento em[!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]  
 Esta seção documenta as alterações de comportamento referentes a recursos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]. Essas alterações também se aplicam a [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
|Problema|DESCRIÇÃO|  
|-----------|-----------------|  
|As pastas de trabalho do SQL Server 2008 R2 PowerPivot não atualizarão os modelos silenciosamente quando forem usadas no SQL Server 2012 SP1 PowerPivot para SharePoint 2013. Portanto, as atualizações de dados agendadas não funcionarão para pastas de trabalho do SQL Server 2008 R2 PowerPivot.|As pastas de trabalho do 2008 R2 serão abertas no [!INCLUDE[ssGeminiShortvnext](../includes/ssgeminishortvnext-md.md)], porém, as atualizações agendadas não funcionarão. Se você revisar o histórico de atualização, verá uma mensagem de erro semelhante à seguinte:<br /> "A pasta de trabalho contém um modelo do PowerPivot sem suporte. O modelo do PowerPivot na pasta de trabalho está no formato do SQL Server 2008 R2 PowerPivot para Excel 2010. Os modelos do PowerPivot com suporte são os seguintes: <br />SQL Server 2012 PowerPivot para Excel 2010<br />SQL Server 2012 PowerPivot para Excel 2013 "<br /><br /> **Como atualizar uma pasta de trabalho:** As atualizações agendadas não funcionarão até que você atualize a pasta de trabalho para uma pasta de trabalho do 2012. Para atualizar a pasta de trabalho e o modelos que ela contém, siga um destes procedimentos:<br /><br /> Baixe e abra a pasta de trabalho no Microsoft Excel 2010 com o suplemento SQL Server 2012 PowerPivot para Excel instalado. Salve a pasta de trabalho e republique-a no servidor do SharePoint.<br /><br /> Baixe e abra a pasta de trabalho no Microsoft Excel 2013. Salve a pasta de trabalho e republique-a no servidor do SharePoint.<br /><br /> <br /><br /> Para obter mais informações sobre a atualização da pasta de trabalho, consulte [Atualizar pastas de trabalho e atualização de dados agendada &#40;SharePoint 2013&#41;](instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).|  
|Alteração de comportamento no DAX [ALL Function](/dax/all-function-dax).|Antes do [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)], se você especificar uma coluna [Data] em Marcar como Tabela de Data, para uso na inteligência de tempo, e se a coluna [Data] for passada como um argumento para a função ALL e, por sua vez, for passada como um filtro para a função CALCULATE, todos os filtros de todas as colunas da tabela serão ignorados, independentemente de qualquer segmentação de dados na coluna de data.<br /><br /> Por exemplo,<br /><br /> `= CALCULATE (<expression>, ALL (DateTable[Date]))`<br /><br /> Antes do [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)], todos os filtros são ignorados em todas as colunas de DateTable, independentemente da coluna [Data] passada como um argumento para a função ALL.<br /><br /> No [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] e no PowerPivot no Excel 2013, o comportamento ignorará os filtros somente na coluna especificada passada como um argumento para a função ALL.<br /><br /> Para corrigir o novo comportamento, ou seja, para ignorar todas as colunas como um filtro em toda a tabela, exclua a coluna [Data] do argumento, por exemplo.<br /><br /> `=CALCULATE (<expression>, ALL(DateTable))`<br /><br /> Isso gerará o mesmo resultado do comportamento anterior ao [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)].|  
  
##  <a name="bkmk_sql2012"></a>Alterações de comportamento em[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 Esta seção documenta as últimas alterações de comportamento referentes a recursos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Essas alterações também se aplicam a [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
### <a name="analysis-services-multidimensional-mode"></a>Analysis Services, Modo Multidimensional  
  
#### <a name="nullprocessing-option-set-to-preserve-is-no-longer-supported-for-distinct-count-measures"></a>A opção NullProcessing definida como Preservar não é suportada para medidas de contagem distintas  
 Antes do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], era possível definir o [elemento NullProcessing &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl) para `Preserve` as medidas de contagem distintas.  Infelizmente, essa prática geralmente produziu resultados inválidos e às vezes até mesmo travou o trabalho de processamento. Como resultado, esta configuração não é válida em [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Tentar usá-lo fará com que o erro de validação a seguir ocorra: "Erros no gerenciador de metadados. Preserve não é um valor de NullProcessing válido para \<a medida de contagem distinta> MeasureName. "  
  
#### <a name="cube-browser-in-management-studio-and-cube-designer-has-been-removed"></a>O navegador de cubos no Management Studio e no Designer de Cubo foi removido  
 O controle de navegador de cubo que o permitiu arrastar e soltar campos em uma estrutura de Tabela Dinâmica no Management Studio ou no Designer de Cubo foi removido do produto. O controle era um componente OWC (Office Web Control). O OWC foi substituído pelo Office e não está mais disponível.  
  
### <a name="powerpivot-for-sharepoint"></a>PowerPivot para SharePoint  
  
#### <a name="higher-permission-requirements-for-using-a-powerpivot-workbook-as-an-external-data-source"></a>Requisitos de permissão mais altos para usar uma pasta de trabalho PowerPivot como uma fonte de dados externa  
 Uma pasta de trabalho do Excel pode renderizar dados PowerPivot inseridos na mesma pasta de trabalho ou em uma pasta de trabalho externa. Na versão anterior, os requisitos de permissão eram os mesmos, independentemente de os dados PowerPivot terem sido inseridos ou serem externos. Se você tivesse permissões **Somente Exibição** em uma pasta de trabalho PowerPivot, poderia obter acesso completo a todos os dados PowerPivot na pasta de trabalho para conexões inseridas e externas.  
  
 Nesta versão, os requisitos de permissão foram alterados para pastas de trabalho do Excel que renderizam dados PowerPivot de um arquivo externo. Nesta versão, você deve ter as permissões **Leitura** (ou, mais especificamente, a permissão **Abrir Itens** ) para se conectar a uma pasta de trabalho PowerPivot externa em um aplicativo cliente. As permissões adicionais especificam que um usuário tem direitos de download para exibir os dados de origem inseridos na pasta de trabalho. As permissões adicionais indicam que os dados do modelo estão inteiramente disponíveis para o aplicativo cliente ou a pasta de trabalho vinculada a ele, resultando em um melhor alinhamento entre os requisitos de permissão e o comportamento real de conexão de dados.  
  
 Para continuar usando uma pasta de trabalho PowerPivot como uma fonte de dados externa, você deve aumentar as permissões do SharePoint para usuários que se conectam a dados PowerPivot externos. Até que você altere as permissões, os usuários receberão o seguinte erro se tentarem acessar pastas de trabalho PowerPivot em uma conexão de fonte de dados: "serviço Web PowerPivot retornou um erro (acesso negado. O documento solicitado não existe ou você não tem permissão para abrir o arquivo.) "  
  
> [!WARNING]  
>  As etapas a seguir instruem você a interromper a herança de permissão no nível da biblioteca e aumentar as permissões do usuário de **Somente Exibição** para **Leitura** em documentos específicos nessa biblioteca. Antes de continuar, examine atentamente as permissões e os documentos existentes e verifique se essas etapas são apropriadas para seu site.  
>   
>  Alternativamente, você pode criar uma pasta na biblioteca, mover todos os documentos afetados para essa pasta e definir permissões exclusivas na pasta.  
  
> [!NOTE]  
>  Se suas pastas de trabalho forem armazenadas na Galeria PowerPivot, a interrupção de herança de permissão em uma pasta de trabalho romperá a geração de imagens em miniatura para essa pasta de trabalho se ela estiver configurada para atualização de dados. Para permitir acesso simultaneamente a pastas de trabalho e a imagens de visualização na galeria, considere conceder permissões de **Leitura** a usuários específicos no nível de biblioteca, para todos os documentos na biblioteca.  
  
 Você deve ser proprietário do site para alterar permissões.  
  
 **Como aumentar permissões no nível de permissão de Leitura para pastas de trabalho individuais**  
  
1.  Clique na seta para baixo para abrir o menu de um documento individual.  
  
2.  Clique em **Gerenciar Permissões**.  
  
3.  Por padrão, uma biblioteca herda permissões. Para alterar as permissões de pastas de trabalho individuais nessa biblioteca, clique em **Parar de Herdar Permissões**.  
  
4.  Marque a caixa de seleção por nomes de usuário ou grupo que requerem permissões adicionais em pastas de trabalho PowerPivot. Permissões adicionais permitirão que esses usuários se vinculem a dados PowerPivot inseridos e usem esses dados como uma fonte de dados externa em outros documentos.  
  
5.  Clique em **Editar Permissões do Usuário**.  
  
6.  Escolha permissões de **Leitura** e clique em **OK**.  
  
#### <a name="powerpivot-gallery-new-rules-for-snapshot-generation-for-some-powerpivot-workbooks"></a>Galeria PowerPivot: novas regras para a geração de instantâneos para algumas pastas de trabalho PowerPivot  
 Esta versão introduz novos requisitos para a geração de imagens de instantâneos na Galeria PowerPivot, eliminando a divulgação de uma potencial fonte de informação (isto é, mostrando um instantâneo de dados de uma fonte de dados para a qual você não tem permissão de exibição). Esses requisitos só se aplicam a pastas de trabalho PowerPivot que se conectam a fontes de dados externas toda vez que você exibir a pasta de trabalho. Se você só usar pastas de trabalho que visualizam dados PowerPivot inseridos, não verá alterações de como os instantâneos são gerados na Galeria PowerPivot.  
  
 Para uma pasta de trabalho que atualiza seus dados sempre que é aberta, os novos requisitos para a geração de instantâneos são os seguintes:  
  
-   As pastas de trabalho PowerPivot usadas como fontes de dados externas por outras pastas de trabalho ou relatórios devem estar na mesma biblioteca que as pastas de trabalho que consomem os dados. Por exemplo, se você tiver sales-data.xlsx que fornece dados a sales-report.xlsx, ambas as pastas de trabalho devem estar nas galeria para que as imagens do instantâneo apareçam.  
  
-   As pastas de trabalho usadas juntas devem herdar permissões de um pai comum (ou seja, da Galeria PowerPivot). Em nosso exemplo, sales-data.xlsx e sales-report.xlsx devem herdar da Galeria PowerPivot.  
  
 Se uma pasta de trabalho não atender a nenhum dos critérios acima, o ícone bloqueado a seguir aparecerá em vez da imagem em miniatura esperada:  
  
 ![GMNI_PowerPivotGalleryIcon_Locked](media/gmni-powerpivotgalleryicon-locked.gif "GMNI_PowerPivotGalleryIcon_Locked")  
  
#### <a name="new-default-setting-for-load-balancing-requests-changed-from-round-robin-to-health-based"></a>Nova configuração padrão para solicitações de balanceamento de carga alteradas de Round Robin para Baseado na Integridade  
 Um aplicativo de serviço PowerPivot tem configurações padrão que determinam como as solicitações de dados PowerPivot são distribuídas por vários servidores PowerPivot para SharePoint em um farm. Na versão anterior, a configuração padrão era **Round Robin**, em que as solicitações eram distribuídas sequencialmente entre os servidores disponíveis. Nesta versão, o padrão agora é **Baseado na Integridade**. O aplicativo de serviço PowerPivot usa estatísticas de integridade de servidor, como a memória ou a CPU disponível, para determinar a instância de servidor que obtém a solicitação xt.  
  
 Se você tiver atualizado seu servidor da versão anterior, o aplicativo de serviço PowerPivot retém a configuração padrão anterior (**Round Robin**). Para usar a configuração do método de alocação **Baseado na Integridade** , modifique as definições de configuração. Para obter mais informações, confira [Create and Configure a PowerPivot Service Application in Central Administration](power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Compatibilidade com versões anteriores](../../2014/getting-started/backward-compatibility.md)   
 [Alterações recentes em recursos do Analysis Services no SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)  
  
  
