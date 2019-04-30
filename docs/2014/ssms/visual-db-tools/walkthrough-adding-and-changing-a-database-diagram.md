---
title: 'Passo a passo: Adicionando e alterando um diagrama de banco de dados | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- database diagrams [SQL Server], about database diagrams
- database diagrams [SQL Server], designing
- database diagrams [SQL Server], creating
ms.assetid: 228caa0d-8f24-46ab-86d1-b6d8631322bc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 59225dd445ec2d075b9c7c8ca7eac52af2020a68
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273741"
---
# <a name="walkthrough-adding-and-changing-a-database-diagram"></a>Passo a passo: Adicionando e alterando um diagrama de banco de dados
  Este passo a passo ilustra como criar e modificar um diagrama de banco de dados e fazer alterações no banco de dados por meio do componente de diagramas de banco de dados. Você verá como adicionar tabelas a diagramas, criar relações entre tabelas, criar restrições e índices em colunas, e alterar o nível das informações exibidas em cada tabela.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]  
  
-   Uma conta com privilégios `dbo` de proprietário de banco de dados  
  
> [!NOTE]  
>  Se você tentar fazer alterações ao usar uma conta sem privilégios suficientes para fazer alterações em tabelas, uma mensagem de erro será exibida.  
  
## <a name="creating-a-diagram"></a>Criando um diagrama  
  
#### <a name="to-create-a-new-database-diagram"></a>Para criar um novo diagrama de banco de dados  
  
1.  No menu **Exibir** , clique em **Pesquisador de Objetos**.  
  
2.  Abra o nó Bancos de dados e abra o nó do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
3.  Clique com o botão direito do mouse no nó Diagramas de Banco de Dados e escolha **Novo Diagrama de Banco de Dados**.  
  
     Se o banco de dados não tiver os objetos necessários para criar diagramas, a seguinte mensagem será exibida: **Este banco de dados não tem um ou mais dos objetos de suporte necessários para usar a diagramação de banco de dados. Deseja criá-los?** Escolha **Sim**.  
  
     A caixa de diálogo **Adicionar Tabela** será exibida.  
  
4.  Selecione **Tipo de Endereço (Pessoa)** e **Endereço (Pessoa)** e clique em **Adicionar**.  
  
     Duas tabelas são adicionadas ao diagrama.  
  
5.  Feche a caixa de diálogo **Adicionar Tabela** .  
  
#### <a name="to-view-different-column-data"></a>Para exibir diferentes dados de coluna  
  
1.  Clique com o botão direito do mouse na tabela `Address` . No menu de atalho, aponte para **Exibição de Tabela**e clique em **Padrão**.  
  
     A grade da tabela mostra três colunas: **Nome da coluna**, **tipo de dados**, e **permitir nulos**.  
  
2.  Clique com o botão direito do mouse na tabela `Address` , clique em **Exibir Tabela** e selecione **Chaves**.  
  
     A grade da tabela mostra uma coluna, com os nomes da coluna da tabela. Somente as colunas que fazem parte dos índices aparecem.  
  
## <a name="creating-new-tables"></a>Criando novas tabelas  
  
#### <a name="to-create-tables-within-diagram-designer"></a>Para criar tabelas dentro do Designer de Diagrama  
  
1.  Clique com o botão direito do mouse no Designer de Diagramas fora das tabelas existentes e escolha **Nova Tabela**.  
  
2.  No **Escolher nome** caixa de diálogo, clique em **Okey** para aceitar o nome padrão `Table1`.  
  
     Uma nova grade de tabela aparece com três colunas: **Nome da coluna**, **tipo de dados**, e **permitir nulos**.  
  
3.  Adicione as seguintes informações para `Table1`:  
  
    |**Nome da coluna**|**Tipo de Dados**|**Permitir Nulos**|  
    |---------------------|-------------------|---------------------|  
    |`T1col1`|`int`|verificado|  
    |`T1col2`|`varchar(50)`|verificado|  
    |`T1col3`|`float`|verificado|  
  
4.  Clique com o botão direito do mouse em `T1col1` e selecione **Definir Chave Primária**.  
  
     Um ícone de chave aparecerá ao lado do nome da coluna.  
  
5.  No menu **Arquivo** , clique em **Salvar Diagrama1**.  
  
6.  No **Escolher nome** caixa de diálogo, clique em **Okey** para aceitar o nome padrão `Diagram1`.  
  
7.  A caixa de diálogo **Save** aparece com uma mensagem informando que `Table1` será salva no banco de dados. Clique em **Sim**.  
  
## <a name="modifying-table-structure"></a>Modificando a estrutura da tabela  
 Você pode adicionar restrições de verificação e fazer relações entre tabelas no Designer de Diagrama.  
  
#### <a name="to-create-check-constraints"></a>Para criar restrições de verificação  
  
1.  Na `Table1`, clique com o botão direito do mouse na linha `T1col3` e escolha **Restrições de Verificação**.  
  
     A caixa de diálogo **Restrições de Verificação** será exibida.  
  
2.  Clique em **Adicionar**.  
  
     Uma nova restrição aparece na lista **Restrição de Verificação Selecionada** , com o nome padrão `CK_Table1`.  
  
3.  Selecione a linha **Expressão** na grade e clique no botão de reticências.  
  
     A caixa de diálogo **Expressão de Restrição de Verificação** é exibida.  
  
4.  Digite `T1col3 > 5` e clique em **OK**.  
  
     `Table1` agora tem uma restrição que todos os valores inseridos em `T1col3` devem ser maior que 5.  
  
5.  Clique em **Fechar**.  
  
#### <a name="to-create-relationships-between-tables"></a>Para criar relações entre tabelas  
  
1.  Crie uma nova tabela no Designer de Diagrama denominada `Table2` com as seguintes colunas:  
  
    |**Nome da coluna**|**Tipo de Dados**|**Permitir Nulos**|  
    |---------------------|-------------------|---------------------|  
    |`T2col1`|`int`|não verificado|  
    |`T2col2`|`varchar(50)`|verificado|  
    |`T2col3`|`xml`|verificado|  
  
    > [!NOTE]  
    >  As colunas no lado da chave primária de uma relação de chave estrangeira devem participar de uma Chave Primária ou de uma Restrição Exclusiva.  
  
2.  Arraste `T2col1` para `T1col1`.  
  
     Duas caixas de diálogo são exibidas: **Relação de chave estrangeira** em segundo plano e **tabelas e colunas** em primeiro plano.  
  
3.  Clique em **OK** para salvar a nova relação.  
  
4.  Clique em **OK** novamente.  
  
## <a name="creating-indexes"></a>Criando índices  
 Você pode criar índices na maioria dos tipos de dados, incluindo XML.  
  
#### <a name="to-create-a-standard-index"></a>Para criar um índice padrão  
  
1.  Clique com o botão direito do mouse na `Table1` e escolha **Índices/Chaves**.  
  
     A caixa de diálogo **Índices/Chaves** é exibida.  
  
2.  Clique em **Adicionar**.  
  
     Um novo índice é exibido na lista **Índice ou Chave Exclusiva/Primária Selecionada** , com um nome padrão similar a `IX_Table1`.  
  
3.  Selecione a linha **Colunas** e clique no botão de reticências.  
  
     A caixa de diálogo **Colunas de Índice** é exibida.  
  
4.  Clique na seta suspensa debaixo de **Nome da Coluna** e selecione `T1col2`.  
  
    > [!NOTE]  
    >  Você pode adicionar outras colunas a esse índice selecionando a célula debaixo de `T1col2` e escolhendo outro nome de coluna.  
  
5.  Clique em **OK** para salvar esse índice.  
  
6.  Clique em **Fechar** na caixa de diálogo **Índices/Chaves** .  
  
#### <a name="to-create-an-xml-index"></a>Para criar um índice XML  
  
1.  Clique com o botão direito do mouse em `T2col1` e escolha **Definir Chave Primária**.  
  
    > [!NOTE]  
    >  Adicionar um índice XML exige que outra coluna na tabela seja definida como uma chave primária clusterizada.  
  
2.  Clique com o botão direito do mouse na linha `T2col3` na `Table2` e selecione **Índices XML**.  
  
     A caixa de diálogo **Índices XML** é exibida.  
  
3.  Clique em **Adicionar**.  
  
     Um índice XML com valores padrão será adicionado à lista **Índice XML Selecionado** .  
  
4.  Clique em **Fechar**.  
  
    > [!NOTE]  
    >  Os índices XML são criados por coluna. O primeiro índice XML é primário; qualquer índice adicional é secundário.  
  
## <a name="saving-the-diagram"></a>Salvando o diagrama  
 Todas as alterações feitas em um diagrama não são postadas ao banco de dados até serem salvas. Se houver problemas ou conflitos, uma caixa de diálogo será exibida com mais informações.  
  
#### <a name="to-save-a-database-diagram"></a>Para salvar um diagrama de banco de dados  
  
1.  No menu **Arquivo** , selecione **Salvar Diagrama1**.  
  
     A caixa de diálogo **Salvar** é exibida. Se a opção **Avisar sobre Tabelas Afetadas** for selecionada, as informações sobre tabelas novas ou alteradas serão listadas.  
  
2.  Clique em **OK**.  
  
3.  Na ocorrência de qualquer erro, a caixa de diálogo **Notificações Pós-salvamento** é exibida com os erros e respectivas causas. Corrija os erros e salve o diagrama novamente.  
  
## <a name="next-steps"></a>Próximas etapas  
 Esse é um diagrama básico somente com duas tabelas existentes e duas tabelas novas, mas ilustra o potencial de diagramação de um banco de dados existente ou de criação de um novo esquema visualmente. Sugestões para exploração adicional incluem:  
  
-   Criar novos diagramas contendo grupos de tabelas relacionadas  
  
-   Personalizar a quantidade de informações mostrada para cada tabela  
  
-   Alterar o layout e adicionar anotações  
  
-   Copiar o diagrama em um bitmap  
  
## <a name="see-also"></a>Consulte também  
 [Personalizar a quantidade de informações exibidas em diagramas &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Configurar o Designer de diagrama de banco de dados &#40;Visual Database Tools&#41;](set-up-database-diagram-designer-visual-database-tools.md)   
 [Adicionar tabelas a diagramas &#40;Visual Database Tools&#41;](add-tables-to-diagrams-visual-database-tools.md)   
 [Criar relações entre tabelas em um diagrama de &#40;Visual Database Tools&#41;](create-relationships-between-tables-on-a-diagram-visual-database-tools.md)   
 [Criar índices XML](../../relational-databases/xml/create-xml-indexes.md)   
 [Copiar uma imagem de um diagrama de banco de dados na área de transferência &#40;Visual Database Tools&#41;](copy-an-image-of-a-database-diagram-to-the-clipboard-visual-database-tools.md)   
 [Trabalhar com layout de diagrama &#40;Visual Database Tools&#41;](work-with-diagram-layout-visual-database-tools.md)  
  
  
