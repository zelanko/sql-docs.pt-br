---
title: 'Tarefa 1: criando uma base de dados de conhecimento e domínios | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f7ad3b085178c0d0cfe3ece010a571992e7fdb99
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064860"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>Tarefa 1: Criando a base de dados de conhecimento e domínios
  Nesta tarefa, você criará a base de dados de conhecimento **suppliers** e criará domínios que são usados para limpeza e dados correspondentes para remover duplicatas.  
  
1.  Iniciar **Data Quality Client**. Clique **em Iniciar**, aponte **para todos os programas**, clique em **Microsoft SQL Server 2012**, clique em **Data Quality Services**e, em seguida, clique em **Data Quality Client**.  
  
2.  Na caixa de diálogo **conectar ao servidor** , selecione a instância do servidor de banco de dados na qual o DQS está instalado e clique em **conectar**.  
  
     ![Caixa de diálogo conectar ao servidor](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "Caixa de diálogo Conectar ao Servidor")  
  
3.  No Data Quality Client home page, no painel **Gerenciamento da base de dados de conhecimento** , clique em **nova base de dados de conhecimento**.  
  
     ![Gerenciamento da Base de Dados de Conhecimento - Novo KB](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "Gerenciamento da Base de Dados de Conhecimento - Novo KB")  
  
4.  Insira **fornecedores** para o **nome** da base de dados de conhecimento.  
  
     ![Nova Base de Dados de Conhecimento - Gerenciamento de Domínio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "Nova Base de Dados de Conhecimento - Gerenciamento de Domínio")  
  
5.  Confirme se **Criar base de dados de conhecimento de** campo está definido como **nenhum** , pois você está criando a base de dados de conhecimento dos **fornecedores** do zero.  
  
6.  Confirme se **Gerenciamento de domínio** está selecionado para a **atividade** e clique em **Avançar**. A atividade Gerenciamento de Domínio permite criar e gerenciar domínios da base de dados de conhecimento.  
  
7.  Na janela **Gerenciamento de domínio** , clique no botão da barra de ferramentas **criar um domínio** para criar um domínio.  
  
     ![Botão de barra de ferramentas Criar Domínio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "Botão de barra de ferramentas Criar Domínio")  
  
8.  Na caixa de diálogo **criar domínio** , digite **ID do fornecedor** para o **nome de domínio**e clique em **OK**.  
  
     ![Caixa de diálogo Criar Domínio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "Caixa de diálogo Criar Domínio")  
  
9. Repita a etapa anterior para criar os domínios a seguir com todas as configurações padrão. Para manter o tutorial simples, você define o **tipo de dados** de todos os domínios como **cadeia de caracteres**. Os outros tipos de dados permitidos são: Inteiro, Decimal e Data. Quando a opção **usar valores principais** é selecionada (padrão), todos os sinônimos são substituídos pelo valor principal do grupo de sinônimos na saída. A configuração da opção **normalizar cadeia de caracteres** (padrão) remove quaisquer caracteres especiais nos valores de domínio. A opção **Formatar saída para** permite selecionar a formatação que é aplicada quando os valores de dados no domínio são gerados. Selecione **habilitar verificador ortográfico** (padrão) para executar o verificador ortográfico em todos os valores de cadeia de caracteres ao popular o domínio. A configuração de **idioma** especifica qual versão de idioma do **Verificador ortográfico** você deseja aplicar. Selecione **desabilitar algoritmos de erro de sintaxe** para popular o domínio sem verificar valores de cadeia de caracteres para erros de sintaxe. Consulte o tópico [criar um domínio](https://msdn.microsoft.com/library/hh510401.aspx) na biblioteca MSDN para obter mais detalhes.  
  
    -   Supplier Name  
  
    -   Email de contato  
  
    -   Linha de Endereço  
  
    -   City  
  
    -   Estado  
  
    -   País  
  
    -   Zip  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 2: Adicionando valores de domínio manualmente](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
