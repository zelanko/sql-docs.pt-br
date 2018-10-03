---
title: Página Propriedades gerais, Shared Datasets (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 10798e41-24c3-4e69-893b-7ee6af7fc958
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 24e303409568f028ff57cf189cad4f1022111e82
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48202726"
---
# <a name="general-properties-page-shared-datasets-report-manager"></a>Página Propriedades Gerais, conjuntos de dados compartilhados (Gerenciador de Relatórios)
  Use a página Conjunto de dados Compartilhado para exibir e gerenciar propriedades para um item de conjunto de dados compartilhado.  
  
 No Gerenciador de Relatórios, você não pode exibir ou alterar a definição de conjunto de dados compartilhado, inclusive a consulta. Para alterar a definição, você deve usar uma ferramenta de criação para abrir e modificar a definição e, em seguida, salvá-la no servidor de relatório.  
  
 Com um conjunto de dados compartilhado, você pode gerenciar as configurações de um conjunto de dados separadamente dos relatórios, componentes e outros itens de catálogo que o usam.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-shared-dataset-properties-page-for-a-shared-dataset"></a>Para abrir a página de propriedades de Conjunto de Dados Compartilhado de um conjunto de dados compartilhado  
  
1.  Abra o Gerenciador de Relatórios e localize o conjunto de dados compartilhado cujas propriedades você deseja configurar.  
  
2.  Focalize o conjunto de dados compartilhado e clique na seta para baixo.  
  
3.  Na lista suspensa, clique em **Gerenciar**. A página Propriedades Gerais será aberta.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite um nome para o conjunto de dados compartilhado que é usado para identificar o item na hierarquia de pastas do servidor de relatório.  
  
 **Descrição**  
 Forneça informações sobre o conjunto de dados compartilhado. Essa descrição é exibida na página Conteúdo.  
  
 **Ocultar na exibição de lista**  
 Selecione essa opção para ocultar o conjunto de dados compartilhado de usuários que estejam usando o modo de exibição de lista no Gerenciador de Relatórios. O modo de exibição de lista é o formato de exibição padrão quando se navega na hierarquia de pastas do servidor de relatórios. Na exibição de lista, os nomes de itens e as descrições fluem pela página. O formato alternativo é a exibição de detalhes. A exibição de detalhes omite descrições, mas contém outras informações sobre o item. Embora seja possível ocultar um item na exibição de lista, você não pode ocultá-lo na exibição de detalhes. Se quiser restringir o acesso a um item, você precisará criar uma atribuição de função.  
  
 **Tempo limite de execução de consulta**  
 Informe o número de segundos até que a consulta expire. Se for 0, a consulta não terá um tempo limite.  
  
 **Aplicar**  
 Salve as alterações.  
  
 **Delete (excluir)**  
 Remove o conjunto de dados compartilhado do banco de dados do servidor de relatório. A exclusão de um conjunto de dados compartilhado desativa qualquer relatório ou versões armazenadas em cache. Para reativar um relatório, você deve abrir cada um em uma ferramenta de criação de relatório e especificar um conjunto de dados com o mesmo nome e a mesma coleção de campos. Como alternativa, você pode atualizar cada referência de região de dados para usar um conjunto de dados diferente com a mesma coleção de campos.  
  
 **Migrar**  
 Realocar um conjunto de dados compartilhado na hierarquia de pastas do servidor de relatório. O clique nesse botão abre a página Mover Itens, na qual você pode navegar até um novo local de pasta. Para obter mais informações, consulte [página Mover itens &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Download**  
 Extraia uma cópia da definição do conjunto de dados compartilhado. Dependendo das associações de arquivo definidas no seu computador, o arquivo será aberto no Visual Studio ou em um aplicativo diferente. Na maioria dos casos, o conjunto de dados compartilhado é aberto como um arquivo XML.  
  
 **Substituir**  
 Substitua a definição do conjunto de dados compartilhado por outra de um arquivo .rsd localizado no sistema de arquivos.  
  
## <a name="see-also"></a>Consulte também  
 [O Gerenciador de relatórios &#40;modo nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Página de conteúdo &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Ajuda de F1 do Gerenciador de relatórios](../../2014/reporting-services/report-manager-f1-help.md)   
 [Opções de atualização de cache &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/cache-refresh-options-report-manager.md)   
 [Página cache, conjuntos de dados de compartilhados &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/caching-page-shared-datasets-report-manager.md)   
 [Gerenciar conjuntos de dados compartilhados](report-data/manage-shared-datasets.md)   
 [Conjuntos de dados compartilhados em cache &#40;SSRS&#41;](report-server/cache-shared-datasets-ssrs.md)  
  
  
