---
title: 'Tarefa 1: Criando uma Base de conhecimento e domínios | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: beec636f9137802c6651f0c08889acf73000b063
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117760"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>Tarefa 1: Criando a base de dados de conhecimento e domínios
  Nesta tarefa, você criará o **fornecedores** da Base de dados de conhecimento e criar domínios que é usado para dados de limpeza e correspondência de dados para remover duplicatas.  
  
1.  Iniciar **cliente Data Quality**. Clique em **iniciar**, aponte para **todos os programas**, clique em **Microsoft SQL Server 2012**, clique em **Data Quality Services**e, em seguida, clique em  **Cliente data Quality**.  
  
2.  No **conectar ao servidor** caixa de diálogo, selecione a instância do servidor de banco de dados no qual o DQS está instalado e clique em **conectar**.  
  
     ![Conecte-se a caixa de diálogo de servidor](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "conectar-se a caixa de diálogo de servidor")  
  
3.  No cliente de qualidade de dados da home page, além de **gerenciamento da Base de dados de Conhecimento** painel, clique em **nova Base de Conhecimento**.  
  
     ![Gerenciamento da Base de dados de Conhecimento - novo KB](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "gerenciamento da Base de dados de Conhecimento - novo KB")  
  
4.  Digite **fornecedores** para **nome** da base de Conhecimento.  
  
     ![Nova Base de Conhecimento - gerenciamento de domínio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "nova Base de Conhecimento - gerenciamento de domínio")  
  
5.  Confirme se **criar Base de dados de Conhecimento de** campo é definido como **nenhum** desde que você está criando o **fornecedores** da base de conhecimento do zero.  
  
6.  Confirme se **gerenciamento de domínio** é selecionado para o **atividade** e clique em **próximo**. A atividade Gerenciamento de Domínio permite criar e gerenciar domínios da base de dados de conhecimento.  
  
7.  No **gerenciamento de domínio** janela, clique em **criar um domínio** botão da barra de ferramentas para criar um domínio.  
  
     ![Criar um botão de barra de ferramentas do domínio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "criar um botão de barra de ferramentas do domínio")  
  
8.  No **criar domínio** caixa de diálogo, digite **Supplier ID** para o **nome de domínio**e clique em **Okey**.  
  
     ![Criar caixa de diálogo domínio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "criar caixa de diálogo de domínio")  
  
9. Repita a etapa anterior para criar os domínios a seguir com todas as configurações padrão. Para manter o tutorial simples, você deve definir o **tipo de dados** de todos os domínios como **cadeia de caracteres**. Os outros tipos de dados permitidos são: Inteiro, Decimal e Data. Quando o **usar valores principais** opção estiver marcada (padrão), todos os sinônimos são substituídos com o valor principal do grupo de sinônimo na saída. Configuração **normalizar cadeia de caracteres** opção (padrão) remove quaisquer caracteres especiais nos valores de domínio. O **formato de saída para** opção permite que você selecione a formatação que será aplicada quando forem gerados os valores de dados no domínio. Selecione **habilitar verificador ortográfico** (padrão) para executar o verificador ortográfico em todos os valores de cadeia de caracteres ao popular o domínio. O **idioma** configuração especifica a versão do idioma do **verificador ortográfico** você deseja aplicar. Selecione **desabilitar algoritmos de erro de sintaxe** para popular o domínio sem verificar os valores de cadeia de caracteres para erros de sintaxe. Consulte [criar um domínio](http://msdn.microsoft.com/library/hh510401.aspx) tópico na biblioteca do MSDN para obter mais detalhes.  
  
    -   Supplier Name  
  
    -   Email de contato  
  
    -   Linha de Endereço  
  
    -   Cidade  
  
    -   Estado  
  
    -   País  
  
    -   CEP  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 2: Adicionando valores de domínio manualmente](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  