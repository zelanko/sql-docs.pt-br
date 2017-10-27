---
title: "Definir parâmetros em um relatório publicado - modo integrado do SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint integration [Reporting Services], content management
- report parameters [Reporting Services]
ms.assetid: dec5d985-a6c1-4dd8-8a66-a848e89a2e18
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ba05b4727499c702b9f8827de9564aad444c1ebc
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="set-parameters-on-a-published-report---sharepoint-integrated-mode"></a>Definir parâmetros em um relatório publicado - modo integrado do SharePoint
  Um relatório parametrizado aceita valores de entrada usados para filtrar dados quando você executa o relatório. Os parâmetros são definidos quando o relatório é criado. Dependendo de como um parâmetro de relatório é configurado na definição do relatório, ele pode aceitar um único valor, vários valores ou valores dinâmicos, que se alteram em resposta a uma seleção anterior (por exemplo, quando você seleciona uma categoria de produto, a próxima seleção pode ser um produto específico dessa categoria). Um parâmetro pode ter um valor padrão, que pode ser usado para executar automaticamente uma versão filtrada do relatório ou pode ser substituído por um valor diferente.  
  
 Essas propriedades podem ser estabelecidas na definição do relatório ou depois que o relatório for publicado. Embora você possa modificar algumas propriedades de parâmetro em uma publicação para alterar o valor e exibir propriedades, você não pode alterar o nome do parâmetro nem o tipo de dados. O nome do parâmetro e o tipo de dados só podem ser alterados pelo autor do relatório na definição do relatório.  
  
 Para executar um relatório com parâmetros, você geralmente deve saber quais valores digitar, embora um relatório possa incluir listas suspensas de valores válidos a serem escolhidos.  
  
 Para definir as propriedades do parâmetro em um relatório publicado, você deve ter a permissão Editar Itens para o relatório. Você pode modificar algumas ou todas as propriedades de parâmetros em um relatório executado de um site do SharePoint. Não é possível personalizar um relatório salvando uma combinação de valores de parâmetros que você queira usar repetidas vezes. Todos os valores padrão que você especificar serão usados por todos os usuários que abrirem o relatório.  
  
 Se o relatório estiver inserido em uma Web Part do Visualizador de Relatórios configurada para sempre mostrar esse relatório, defina as propriedades na Web Part do Visualizador de Relatórios. Para obter mais informações, consulte [Adicionar a Web Part do Visualizador de Relatórios a uma página da Web &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md).  
  
### <a name="to-run-a-parameterized-report"></a>Para executar um relatório com parâmetros  
  
1.  Abra a biblioteca que contém o relatório.  
  
2.  Clique no nome do relatório. Você deve saber com antecedência quais relatórios têm parâmetros. Não há nenhum identificador visual no relatório para indicar se ele tem parâmetros.  
  
3.  Quando o relatório for aberto, especifique os parâmetros que quer usar. A área de Parâmetros pode estar visível, recolhida ou oculta dependendo de como as propriedades foram definidas na Web Part do Visualizador de Relatórios.  
  
    1.  Se a área de Parâmetros estiver visível, escolha um valor para cada parâmetro.  
  
    2.  Se houver uma estreita faixa colorida ao longo do comprimento do relatório com uma seta no meio, a área de Parâmetros estará recolhida. Você pode clicar na seta para expandi-la.  
  
    3.  Se a área de Parâmetros estiver oculta, não será possível especificar um valor.  
  
4.  Clique em **Aplicar** na parte inferior da área de Parâmetros para executar o relatório.  
  
     É possível especificar uma combinação de valores que não gerem o resultado esperado. Pode ser necessário que o autor do relatório o modifique se você não estiver obtendo as informações de que precisa.  
  
5.  Clique em **OK**.  
  
### <a name="to-set-parameter-properties"></a>Para definir propriedades de parâmetros  
  
1.  Abra a biblioteca ou pasta que contém o relatório.  
  
2.  Aponte para o relatório e clique na seta para baixo.  
  
3.  Clique em **Gerenciar Parâmetros**. Se o relatório contiver parâmetros, cada um deles será listado na página. A lista mostra o nome do parâmetro, o tipo de dados e o valor de dados usado por padrão e se ele está visível na área de parâmetros quando você abre o relatório.  
  
4.  Clique em um parâmetro na lista para modificar suas configurações.  
  
5.  Em Valor Padrão, digite um valor para o parâmetro. O valor não será validado, portanto, certifique-se de inserir um valor adequado ao relatório.  
  
    1.  Escolha **Usar expressão de valor especificado na definição de relatório** se quiser usar o valor padrão definido quando o relatório foi criado. Se a definição de relatório não fornecer um valor padrão, essa opção estará indisponível.  
  
    2.  Escolha **Substituir o valor padrão de relatório** se quiser especificar uma substituição para o valor padrão de definição de relatório. Opcionalmente, para parâmetros de relatório que aceitam valores nulos, você pode marcar a caixa de seleção **Nulo** para evitar a filtragem com base no parâmetro.  
  
    3.  Escolha **O parâmetro não tem um valor padrão** se quiser que cada usuário especifique um valor antes de o relatório ser processado. Se você selecionar essa opção, deve definir configurações de exibição que solicitem que o usuário especifique um valor.  
  
     Observe que se todos os valores de parâmetros tiverem um valor padrão, o relatório será executado automaticamente com esses valores quando o usuário o abrir. Porém, se a área de parâmetros for exibida, os usuários poderão substituir o valor padrão e executar o relatório novamente.  
  
6.  Defina as opções de exibição para determinar se o parâmetro será visível.  
  
    1.  Escolha **Avisar Usuário** para mostrar o parâmetro na página. Você pode especificar o texto do prompt que aparece no campo para fornecer uma breve instrução sobre o formato ou tipo de dados que o usuário deve fornecer.  
  
    2.  Escolha **Oculto** se você estiver usando um valor padrão e não quiser que o parâmetro seja visível na área de Parâmetros.  
  
    3.  Escolha **Interno** se estiver usando um valor padrão e não quiser que o parâmetro seja visível na área de Parâmetros ou em páginas de assinatura.  
  
7.  Clique em **Aplicar**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência à permissão de listas e sites do SharePoint para itens do servidor de relatório](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
  
  

