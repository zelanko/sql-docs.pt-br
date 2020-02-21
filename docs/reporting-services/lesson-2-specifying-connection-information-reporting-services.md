---
title: 'Lição 2: Especificar informações de conexão (Reporting Services) | Microsoft Docs'
description: 'Nesta lição, você definirá uma fonte de dados: as informações de conexão que o relatório usa para acessar dados de um banco de dados relacional ou de outras fontes.'
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9d4e12a0322a35e96bd930c4fa6f1f852daf2bdd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75258459"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>Lição 2: Especificar informações de conexão (Reporting Services)

Na lição 1, você adicionou um relatório paginado do [!INCLUDE[ssrsnoversion-md](../includes/ssrsnoversion-md.md)] ao seu projeto do Tutorial.
  
Nesta lição, você definirá uma *fonte de dados*, as informações de conexão que o relatório usa para acessar dados de um banco de dados relacional ou de outras fontes.

Neste relatório, você adicionará o banco de dados de exemplo AdventureWorks2016 como sua fonte de dados. Este tutorial assume que esse banco de dados está localizado na instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] instalada no computador local.  

## <a name="to-set-up-a-connection"></a>Para configurar uma conexão  

1. No painel **Dados do Relatório**, selecione **Nova** > **Fonte de Dados**. Se o painel **Dados do Relatório** não estiver visível, selecione o menu **Exibição** > **Dados de Relatório**.

    ![ssrs-table-tutorial-2-new-data-source](media/ssrs-table-tutorial-2-new-data-source.png)

    A caixa de diálogo **Propriedades da Fonte de Dados** é aberta exibindo a seção **Geral**.

    ![Caixa de diálogo Propriedades da Fonte de Dados](media/lesson-2-specifying-connection-information-reporting-services/vs-datasource-connection-properties-dialog-box.png)

2. Na caixa de texto **Nome**, digite "AdventureWorks2016".

3. Selecione o botão de opção **Conexão inserida**.

4. Na caixa de seleção suspensa **Tipo**, selecione "Microsoft SQL Server".
  
5. Na caixa de texto **Cadeia de conexão**, digite a seguinte cadeia de caracteres:

    `Data source=localhost; initial catalog=AdventureWorks2016`

    > [!NOTE]
    > Esta cadeia de conexão assume que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], o servidor de relatório, e o banco de dados AdventureWorks2016 estão instalados no computador local.
    >
    >Altere a cadeia de conexão e substitua o "localhost" pelo nome do seu servidor/instância do banco de dados se a suposição não for verdadeira. Se estiver usando [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] ou uma instância nomeada do SQL Server, você precisará modificar a cadeia de conexão para incluir as informações da instância. Por exemplo:
    >
    > `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2016`
    >
    > Para obter mais informações sobre cadeias de conexão, você pode conferir a seção `See also` abaixo.

6. Selecione a guia **Credenciais** e, na seção **Alterar as credenciais usadas para se conectar à fonte de dados**, selecione o botão de opção **Usar a Autenticação do Windows (segurança integrada)** .

7. Selecione **OK** para concluir o processo.

O Designer de Relatórios adiciona a fonte de dados AdventureWorks2016 no painel **Dados de Relatório**.

![ssrs-adventureworks-datasource](media/lesson-2-specifying-connection-information-reporting-services/ssrs-adventureworks-datasource2016.png)

## <a name="next-steps"></a>Próximas etapas

Nesta lição, você definiu com êxito uma conexão ao banco de dados de exemplo AdventureWorks2016. Continue com a [Lição 3: Como definir um conjunto de dados para o relatório de tabela &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md) para definir um conjunto de dados para o relatório.

## <a name="see-also"></a>Confira também

[Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS](report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)
