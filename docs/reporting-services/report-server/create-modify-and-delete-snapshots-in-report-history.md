---
title: "Criar, modificar e excluir instantâneos no histórico de relatório | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [Reporting Services]
- report snapshots [Reporting Services]
ms.assetid: 5aebbbfa-a8db-462d-8ab9-746fad9525f0
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4c3d0de81994b5a234ead420277718c760f9ddb3
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="create-modify-and-delete-snapshots-in-report-history"></a>Criar, modificar e excluir instantâneos no histórico de relatório
  O histórico de relatórios é uma coleção de instantâneos de relatório. Você pode manter o histórico de relatórios adicionando e excluindo instantâneos ou modificando propriedades que afetam o armazenamento do histórico de relatórios. O histórico de relatórios pode ser criado manualmente ou em uma agenda.  
  
 Para criar o histórico de relatórios, sua atribuição de função deve incluir a tarefa “Gerenciar histórico de relatórios”. Para exibir o histórico de relatórios, sua atribuição de função deve incluir a tarefa “Exibir relatórios”. O histórico de relatórios está disponível a todos os usuários que têm acesso ao relatório. Você não pode habilitar ou desabilitar o histórico de relatórios seletivamente para um subconjunto de usuários.  
  
 Os instantâneos do histórico de relatórios são identificados pela data e hora em que foram criados. A data e a hora são baseadas no momento em que a consulta foi executada.  
  
## <a name="creating-snapshots-in-report-history"></a>Criando instantâneos no histórico de relatórios  
 Os instantâneos podem ser criados manualmente ou em intervalos agendados para qualquer relatório que possa ser executado de modo autônomo. Para ser executado de modo autônomo, o relatório deve usar credenciais armazenadas ou nenhuma credencial. Além disso, se o relatório usar parâmetros, você deve especificar valores padrão a serem usados quando o relatório for executado. Você pode especificar credenciais armazenadas e valores de parâmetro nas páginas de propriedade do relatório. Para obter mais informações, consulte [Página Propriedades do Parâmetro &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/ebb53598-2378-46ae-8935-d5192f8ea49a).  
  
 Ao criar um instantâneo de relatório, os seguintes elementos são armazenados junto com o instantâneo no banco de dados do servidor de relatório:  
  
-   O conjunto de resultados (isto é, os dados do relatório recuperados através das credenciais especificadas na página de propriedades Fontes de Dados do relatório).  
  
-   A definição de relatório subjacente, conforme existia na ocasião em que o instantâneo foi criado. Se a definição de relatório for modificada subsequentemente após a geração do instantâneo, as alterações não serão refletidas no instantâneo.  
  
-   Valores de parâmetro usados para obter ou filtrar o conjunto de resultados.  
  
-   Recursos internos, como imagens. Os recursos externos que são vinculados a um relatório não são armazenados com o instantâneo de relatório.  
  
 As configurações determinam como o histórico de relatórios pode ser criado e o número de instantâneos de relatório que podem ser armazenados.  
  
 Se um relatório produzir um erro, um instantâneo não será criado. Os relatórios que produzem avisos, enquanto ainda forem executados, podem ser usados para gerar instantâneos.  
  
## <a name="modifying-properties-and-deleting-report-history"></a>Modificando propriedades e excluindo o histórico de relatórios  
 Após ser criado, não é possível modificar o instantâneo de relatório. No entanto, você pode modificar propriedades de modo que o histórico de relatórios seja excluído.  
  
 O histórico de relatórios pode ser excluído dos seguintes modos:  
  
-   Exclua manualmente os instantâneos de modo individual ou em grupos.  
  
     Você pode excluir instantâneos da página Histórico no Gerenciador de Relatórios. Navegue até o relatório, clique em Histórico, marque a caixa de seleção ao lado dos instantâneos que deseja excluir e clique em **Excluir**.  
  
-   Diminua o limite do histórico de relatórios para reduzir o número de instantâneos que são armazenados. O limite do histórico de relatórios pode ser definido para o servidor de relatório ou para relatórios específicos. Quando o limite é abaixado, os instantâneos mais antigos são excluídos do histórico.  
  
 Você não pode excluir todo o histórico de relatórios armazenado em um servidor de relatório em uma operação em massa.  
  
 O histórico de relatórios também é excluído quando você exclui um relatório. Por exemplo, se você excluir um relatório de vendas mensais porque está substituindo esse relatório por uma versão mais recente, todo o histórico associado ao relatório também será excluído. No entanto, se você mover um relatório, todo o histórico de relatórios também será movido.  
  
## <a name="see-also"></a>Consulte também  
 [Criar histórico de relatório &#40; O Reporting Services no SharePoint integrado modo &#41;](../../reporting-services/report-server/create-report-history-reporting-services-in-sharepoint-integrated-mode.md)   
 [Gerenciador de relatórios &#40; Modo nativo do SSRS &#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Gerenciamento de conteúdo de servidor de relatório e &#40; Modo nativo do SSRS &#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Adicionar um instantâneo para o relatório histórico de &#40; Gerenciador de relatórios &#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Limitar o histórico de relatório &#40; Gerenciador de relatórios &#41;](../../reporting-services/reports/limit-report-history-report-manager.md)  
  
  
