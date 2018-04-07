---
title: Definindo opções de migração (AccessToSQL) e conversão | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 747a70560aaa3710429bb8708699dfa2dff9234b
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>Conversão de configuração e opções de migração (AccessToSQL)
Para cada projeto SSMA, você pode definir opções de nível de projeto. Essas opções especificam como os objetos são convertidos, como os dados são migrados e como os tipos de dados de origem são mapeados para tipos de dados de destino. Antes de converter objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure ou migrar dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, verifique se as opções de configuração são adequadas para o projeto.  
  
## <a name="configuration-options-and-modes"></a>Modos e opções de configuração  
O SSMA tem quatro conjuntos de configurações e quatro modos para definir essas configurações: padrão, Optimistic, completo e personalizado. O padrão é recomendado para a maioria dos usuários. Use o modo otimista para conversões simples. Use o modo completo se você quiser ver todas as mensagens. No modo personalizado, você deve definir as opções.  
  
As configurações são descritas na seção "Referência de Interface de usuário" desta documentação. Para obter mais informações sobre as configurações e como as configurações são aplicadas em cada modo, consulte os tópicos a seguir:  
  
-   [Configurações do projeto (conversão)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [Configurações do projeto (migração)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [Configurações do projeto (GUI)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Configurações do projeto (mapeamento de tipo)](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [Configurações de projeto (SQL Azure)](http://msdn.microsoft.com/en-us/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>Definindo opções de projeto  
Em SSMA, você pode configurar as configurações padrão para todos os projetos. Essas configurações são salvas no arquivo de configuração do SSMA e aplicadas a qualquer novo projeto que você criar.  
  
**Para definir opções de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações de projeto padrão**.  
  
2.  No **configurações de projeto padrão** caixa de diálogo, siga um destes procedimentos:  
  
    -   Selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido e alterado de **versão de destino de migração** lista suspensa, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **conversão ou migração ou SQL Azure**.  
  
        > [!NOTE]  
        > Opção do SQL Azure está disponível a **geral** guia somente se o tipo de projeto criado é do SQL Azure.  
  
    -   Para selecionar um modo predefinido, selecione **padrão**, **Optimistic**, ou **completo** no **modo** caixa suspensa.  
  
    -   Para especificar um modo personalizado, selecione **personalizado** no **modo** caixa, selecione uma opção no painel esquerdo, clique na configuração ou o valor no painel direito e, em seguida, selecione ou digite a nova configuração ou o valor.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
Você também pode personalizar configurações para o projeto atual. Essas configurações são salvas no arquivo de projeto atual.  
  
**Para personalizar as configurações para o projeto atual**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações de projeto**.  
  
2.  No **configurações de projeto** caixa de diálogo, siga um destes procedimentos:  
  
    -   Para selecionar um modo predefinido, selecione **padrão**, **Optimistic**, ou **completo** no **modo** caixa suspensa.  
  
    -   Para especificar um modo personalizado, selecione **personalizado** no **modo** caixa, selecione uma opção no painel esquerdo, clique na configuração ou o valor no painel direito e, em seguida, selecione ou digite a nova configuração ou o valor.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [tipos de dados de destino e origem do mapeamento](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)  
  
-   Para personalizar o mapeamento de bancos de dados de origem e de destino, consulte [bancos de dados de destino e origem do mapeamento](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
-   Caso contrário, você pode converter as definições de objeto de banco de dados do Access em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou definições de objeto do SQL Azure. Para obter mais informações, consulte [converter objetos de banco de dados do Access](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
