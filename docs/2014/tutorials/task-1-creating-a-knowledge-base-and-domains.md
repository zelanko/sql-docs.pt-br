---
title: 'Tarefa 1: Criando uma Base de conhecimento e domínios | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 79edd8566f2b3c9b586bc8c8815e1d9bc586fb05
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481240"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>Tarefa 1: Criar a base de dados de conhecimento e domínios
  Nesta tarefa, você cria o **fornecedores** da Base de dados de conhecimento e criar domínios que é usado para dados de limpeza e correspondência de dados para remover duplicatas.  
  
1.  Inicie **cliente Data Quality**. Clique em **inicie**, aponte para **todos os programas**, clique em **Microsoft SQL Server 2012**, clique em **Data Quality Services**e, em seguida, clique em  **Cliente data Quality**.  
  
2.  No **conectar ao servidor** caixa de diálogo, selecione a instância do servidor de banco de dados no qual o DQS está instalado e clique em **Connect**.  
  
     ![Conectar-se a caixa de diálogo do servidor](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "conectar-se a caixa de diálogo do servidor")  
  
3.  No cliente de qualidade de dados da home page, além de **gerenciamento da Base de dados de Conhecimento** painel, clique em **nova Base de Conhecimento**.  
  
     ![Gerenciamento da Base de dados de Conhecimento - novo KB](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "gerenciamento da Base de dados de Conhecimento - novo KB")  
  
4.  Insira **fornecedores** para **nome** da base de dados de Conhecimento.  
  
     ![Nova Base de Conhecimento - gerenciamento de domínio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "nova Base de Conhecimento - gerenciamento de domínio")  
  
5.  Confirme se **criar Base de dados de Conhecimento de** campo é definido como **None** uma vez que você está criando o **fornecedores** base de dados de conhecimento do zero.  
  
6.  Confirme **gerenciamento de domínio** está selecionado para o **atividade** e clique em **próxima**. A atividade Gerenciamento de Domínio permite criar e gerenciar domínios da base de dados de conhecimento.  
  
7.  No **gerenciamento de domínio** janela, clique em **criar um domínio** botão de barra de ferramentas para criar um domínio.  
  
     ![Criar um botão de barra de ferramentas do domínio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "criar botão de barra de ferramentas do domínio")  
  
8.  No **criar domínio** caixa de diálogo, digite **Supplier ID** para o **nome de domínio**e clique em **Okey**.  
  
     ![Criar caixa de diálogo do domínio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "criar caixa de diálogo do domínio")  
  
9. Repita a etapa anterior para criar os domínios a seguir com todas as configurações padrão. Para simplificar o tutorial, você deve definir a **tipo de dados** de todos os domínios como **cadeia de caracteres**. Os outros tipos de dados permitidos são: Número inteiro, Decimal e data. Quando o **usar valores principais** opção estiver marcada (padrão), todos os sinônimos são substituídos pelo valor principal do grupo de sinônimos na saída. Definindo **cadeia de caracteres normalizar** opção (padrão) remove caracteres especiais nos valores de domínio. O **formato de saída para** opção permite que você selecione a formatação é aplicada quando forem gerados os valores de dados no domínio. Selecione **habilitar verificador ortográfico** (padrão) para executar o verificador ortográfico em todos os valores de cadeia de caracteres ao popular o domínio. O **linguagem** configuração especifica qual versão do idioma a **verificador ortográfico** você deseja aplicar. Selecione **desabilitar algoritmos de erro de sintaxe** para popular o domínio sem verificar os valores de cadeia de caracteres para erros de sintaxe. Ver [criar um domínio](https://msdn.microsoft.com/library/hh510401.aspx) tópico na biblioteca MSDN para obter mais detalhes.  
  
    -   Supplier Name  
  
    -   Email de contato  
  
    -   Linha de Endereço  
  
    -   Cidade  
  
    -   Estado  
  
    -   País  
  
    -   CEP  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 2: Adicionando valores de domínio manualmente](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
