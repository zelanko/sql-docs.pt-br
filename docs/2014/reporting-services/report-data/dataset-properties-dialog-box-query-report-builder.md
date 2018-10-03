---
title: Caixa de diálogo Propriedades do Conjunto de Dados, Consulta (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10024"
ms.assetid: 75432318-0b00-4797-917c-0a2e74f9d951
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 30dea5e6c9df6f1bd7f22d0ff37ca8800b21b095
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132986"
---
# <a name="dataset-properties-dialog-box-query-report-builder"></a>Caixa de diálogo Propriedades do Conjunto de Dados, Consulta (Construtor de Relatórios)
  Selecione **Consulta** na caixa de diálogo **Propriedades do Banco de Dados** para escolher um conjunto de dados compartilhado de um servidor de relatório ou criar um conjunto de dados inserido. Para um conjunto de dados inserido, você deve escolher uma fonte de dados e criar uma consulta.  
  
 A caixa de diálogo **Propriedades do Conjunto de Dados** inclui o seguinte:  
  
-   [Caixa de diálogo Propriedades do Conjunto de Dados, Parâmetros &#40;Construtor de Relatórios&#41;](../dataset-properties-dialog-box-parameters-report-builder.md)  
  
-   [Caixa de diálogo Propriedades do Conjunto de Dados, Campos &#40;Construtor de Relatórios&#41;](../dataset-properties-dialog-box-fields-report-builder.md)  
  
-   [Caixa de diálogo Propriedades do Conjunto de Dados, Opções &#40;Construtor de Relatórios&#41;](dataset-properties-dialog-box-options-report-builder.md)  
  
-   [Caixa de diálogo Propriedades do Conjunto de Dados, Filtros &#40;Construtor de Relatórios&#41;](../dataset-properties-dialog-box-filters-report-builder.md)  
  
 Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite um nome para o conjunto de dados. O nome não pode ser igual a um nome de alguma região de dados ou grupo no relatório.  
  
 **Usar um conjunto de dados compartilhado**  
 Selecione esta opção para usar um conjunto de dados predefinido do servidor de relatório.  
  
 **Procurar**  
 Vá até uma pasta em um servidor de relatório ou site do SharePoint e selecione um conjunto de dados compartilhado (.rsd).  
  
 **Usar um conjunto de dados inserido em meu relatório**  
 Selecione essa opção para criar um conjunto de dados a ser usado apenas por esse relatório.  
  
 **Fonte de dados**  
 Selecione a fonte de dados na qual deseja basear o conjunto de dados. Para criar uma nova fonte de dados, clique em **Novo**.  
  
 **Tipo de consulta**  
 Selecione o tipo de comando ou consulta que deseja usar no conjunto de dados. Selecione **Texto** para executar uma consulta para recuperar dados do banco de dados. Selecione **Tabela** para usar o recurso **TableDirect** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para selecionar todos os campos de uma tabela. Selecione **Procedimento Armazenado** para executar um procedimento armazenado pelo nome. **Texto** é selecionado por padrão e é usado para a maioria das consultas. Para editar a consulta de fonte de dados selecionada, clique em **Designer de Consulta**.  
  
> [!NOTE]  
>  Nem todos os tipos de consulta são suportados por todas as fontes de dados. Por exemplo, **Tabela** é suportado somente pelos tipos de fonte de dados **OLE DB** e **ODBC**.  
  
 **Consulta**  
 Esta opção é exibida quando você escolhe o tipo de comando **Texto** . Digite uma consulta ou importe uma consulta preexistente clicando em **Importar**. Clique no botão **Expressão** (*fx*) para editar a expressão.  
  
> [!NOTE]  
>  Se você usou um designer de consulta para criar uma consulta, o texto da consulta será exibido nesta caixa.  
  
 **Nome da tabela**  
 Digite o nome da tabela que deseja usar como um conjunto de dados. Esta opção é exibida quando você seleciona **Tabela**.  
  
 **Selecionar ou digitar nome do procedimento armazenado**  
 Digite ou escolha o nome do procedimento armazenado que deseja usar. Clique no botão **Expressão** (*fx*) para editar a expressão. Esta opção é exibida quando você escolhe o tipo de comando Procedimento Armazenado.  
  
 **Tempo limite (em segundos)**  
 Informe o número de segundos até que a consulta expire. O padrão é 30 segundos. O valor para **Tempo Limite** deve ser vazio ou maior que zero. Se for vazio, a consulta não terá um tempo limite.  
  
 **Atualizar Campos**  
 Execute o comando query para atualizar a lista de campos na página [Caixa de Diálogo Propriedades do Conjunto de Dados, Campos](../dataset-properties-dialog-box-fields-report-builder.md) .  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-datasets-ssrs.md)   
 [Ajuda do Construtor de Relatórios para caixas de diálogo, painéis e assistentes](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Designers de Consultas &#40;Construtor de Relatórios&#41;](../query-designers-report-builder.md)  
  
  
