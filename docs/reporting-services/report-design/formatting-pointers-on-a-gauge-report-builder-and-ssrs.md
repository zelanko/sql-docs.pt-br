---
title: "Formatando ponteiros em um medidor (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2fdf670a-5237-48fe-813d-97657c5c77d2
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: eaee62d06fd3ab67d10b64cb44282377ace28914
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="formatting-pointers-on-a-gauge-report-builder-and-ssrs"></a>Formatando ponteiros de um medidor (Construtor de Relatórios e SSRS)
 Em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , um ponteiro do medidor indica o valor atual do medidor.   
   
 Por padrão, quando um campo for adicionado, os valores contidos nele serão agregados a um valor mostrado pelo ponteiro do medidor. É possível adicionar vários ponteiros ao medidor para mostrar vários valores na mesma escala, ou adicionar várias escalas e um ponteiro para todas as escalas adicionadas. Depois de adicionar um campo a um medidor, defina os valores mínimo e máximo da escala correspondente para oferecer contexto ao valor do ponteiro. Outra opção é definir os valores mínimo e máximo em um intervalo, que mostra uma área crítica na escala.  
  
 É possível definir propriedades de aparência no ponteiro, clicando com o botão direito do mouse no ponteiro e selecionando **Propriedades de Ponteiro Radial** ou **Propriedades de Ponteiro Linear**. Cada ponteiro do medidor contém o mesmo conjunto de propriedades. Também há propriedades de aparência correspondentes exclusivas de cada tipo de medidor:  
  
-   Em um medidor radial, é possível especificar um ponteiro e uma extremidade de agulha.  
  
-   Em um medidor linear, você pode especificar um ponteiro de termômetro, que é uma variação do ponteiro de barra. O ponteiro de termômetro permite que você especifique a forma do bulbo.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="HowPointer"></a> Como o ponteiro é conectado a dados  
 Por padrão, quando adicionado, um medidor contém um ponteiro sem campo associado. Isso é conhecido como ponteiro vazio. Ele exibirá zero até que um campo seja adicionado ao painel de dados. Quando você adiciona um campo ao painel de dados, o ponteiro é conectado a esse campo. Caso você exclua um campo do painel de dados, o ponteiro associado a esse campo também será excluído.  
  
 Depois de adicionar os dados, quando clicar com o botão direito do mouse no ponteiro, você obterá as opções **Limpar Valor do Ponteiro** e **Excluir Ponteiro** . A opção **Limpar Valor do Ponteiro** removerá o campo anexado ao medidor, mas o ponteiro continuará aparecendo no medidor. A opção **Excluir Ponteiro** removerá o campo do medidor e excluirá o ponteiro da exibição. Se você adicionar novamente um campo ao medidor, o ponteiro padrão reaparecerá. Quando você define a propriedade **Hidden** como **True**, o ponteiro não permanece oculto na superfície de design, embora continue oculto em tempo de execução.  
  
##  <a name="DisplayingMultiple"></a> Exibindo vários ponteiros no medidor  
 É possível adicionar vários ponteiros ao medidor para apontar para vários valores na mesma escala. Isso pode ser útil para mostrar valores baixo e alto simultaneamente. Para especificar mais de um ponteiro do medidor na mesma escala, clique com o botão direito do mouse em qualquer lugar do medidor e clique em **Adicionar Ponteiro** no menu de atalho. Também é possível adicionar uma escala clicando com o botão direito do mouse em qualquer lugar do medidor e clicando em **Adicionar Escala**. Assim, você pode adicionar um ponteiro e ele será associado automaticamente à última escala.  
  
 Quando os ponteiros se sobrepõem, a ordem de desenho dos ponteiros é determinada pela ordem na qual eles são adicionados ao medidor. Não é possível reorganizar a ordem de desenho dos ponteiros alterando a ordem dos campos no painel de dados. Para alterar a ordem do desenho de vários ponteiros, abra o painel Propriedades e clique em **Ponteiros (…)**. Em seguida, altere a ordem dos ponteiros na coleção Ponteiro.  
  
##  <a name="SettingGradients"></a> Definindo as gradações em uma extremidade de agulha  
 Você pode especificar uma extremidade de agulha que possa ser desenhada acima ou abaixo do ponteiro apenas em um ponteiro radial. Todos os estilos de extremidade de agulha são desenhados usando gradações internas que não podem ser modificadas. A exceção é o estilo **RoundedDark** , em que você pode especificar uma cor de gradiente e o estilo de gradiente.  
  
##  <a name="SettingSnappingInterval"></a> Como definir um intervalo de ajuste  
 Um intervalo de ajuste define o múltiplo para o qual os valores são arredondados. Por padrão, o medidor apontará para o valor exato do campo especificado no painel de dados. No entanto, talvez você queira arredondar o valor exato para cima ou para baixo de forma que o ponteiro se ajuste a um intervalo predefinido. Por exemplo, se o valor em seu medidor for 34,2 e você especificar um intervalo de ajuste de 5, o ponteiro do medidor apontará para 35. Se o valor em seu medidor for 31,2 e você especificar um intervalo de ajuste de 5, o ponteiro do medidor apontará para 30. Para obter mais informações, consulte [Definir um intervalo de ajuste em um medidor (Construtor de Relatórios e SSRS)](http://msdn.microsoft.com/en-us/0ece7297-6e2f-47fb-835d-b9e9cce53fe2).  
  
##  <a name="SpecifyingImage"></a> Especificando uma imagem como um ponteiro em um medidor radial  
 Além da lista interna dos estilos de ponteiro, é possível especificar uma imagem como um ponteiro. Isso é muito efetivo quando você usa uma imagem para substituir um estilo de ponteiro de agulha existente. A imagem é sobreposta no ponteiro, mas toda a funcionalidade de ponteiro é aplicável. As opções de cor e de gradação não são aplicáveis quando uma imagem é usada no ponteiro.  
  
 Caso a forma da imagem do ponteiro seja irregular, você deve definir a cor como transparente para ocultar as áreas da imagem que não devem ser exibidas no medidor. Quando você define uma cor transparente, o medidor transpõe a imagem no ponteiro existente e corta a imagem para que apenas a forma do ponteiro seja exibida. O medidor redimensiona a imagem para ajustar o tamanho do ponteiro. Quando você especificar uma imagem de um ponteiro, todos os ponteiros subsequentes adicionados acima do medidor serão desenhados abaixo da imagem. Por esse motivo, é melhor não especificar uma imagem para o ponteiro caso haja vários ponteiros no medidor. Para obter mais informações, consulte [Especificar uma imagem como um ponteiro em um medidor (Construtor de Relatórios e SSRS)](http://msdn.microsoft.com/en-us/9d73b3c3-a068-4868-a2be-0cd261b6e92b).  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando escalas em um medidor &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formatando intervalos de um medidor &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-ranges-on-a-gauge-report-builder-and-ssrs.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
