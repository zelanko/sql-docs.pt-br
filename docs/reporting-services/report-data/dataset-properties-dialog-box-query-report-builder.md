---
title: Caixa de diálogo Propriedades do Conjunto de Dados, Consulta (Construtor de Relatórios) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: reference
f1_keywords:
- "10024"
- sql13.rtp.rptdesigner.datasetproperties.query.f1
- "10160"
ms.assetid: 75432318-0b00-4797-917c-0a2e74f9d951
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e05ae59d963bd9b165d2f6f825955ee276683328
ms.sourcegitcommit: 1800fc15075bb17b50d0c18b089d8a64d87ae726
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66500450"
---
# <a name="dataset-properties-dialog-box-query-report-builder"></a>Caixa de diálogo Propriedades do Conjunto de Dados, Consulta (Construtor de Relatórios)
 
Selecione **Consulta** na caixa de diálogo **Propriedades do Banco de Dados** para escolher um conjunto de dados compartilhado de um servidor de relatório ou criar um conjunto de dados inserido. Para um conjunto de dados inserido, você deve escolher uma fonte de dados e criar uma consulta.  
  
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
>  Se você usa um designer de consulta para criar uma consulta, o texto da consulta é exibido nesta caixa.  
  
**Nome da tabela**  
Esta opção é exibida quando você seleciona **Tabela**. Digite o nome da tabela que deseja usar como um conjunto de dados.   
  
**Selecionar ou digitar nome do procedimento armazenado**  
Esta opção é exibida quando você escolhe o tipo de comando Procedimento Armazenado. Digite ou escolha o nome do procedimento armazenado que deseja usar. Clique no botão **Expressão** (*fx*) para editar a expressão.   
  
 **Tempo limite (em segundos)**  
 Informe o número de segundos até que a consulta expire. O padrão é 30 segundos. O valor para **Tempo Limite** deve ser vazio ou maior que zero. Se for vazio, a consulta não terá um tempo limite.  
  
 **Atualizar Campos**  
 Execute o comando query para atualizar a lista de campos na página **Caixa de Diálogo Propriedades do Conjunto de Dados, Campos**.  
  
## <a name="see-also"></a>Consulte Também  
[Conjuntos de dados inseridos e compartilhados de relatório (Construtor de Relatórios e SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
[Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
[Ferramentas de Design da Consulta &#40;SSRS&#41;](query-design-tools-ssrs.md)  
  
  
