---
title: Definindo opções de migração (AccessToSQL) e conversão | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.openlocfilehash: bf73284de3f23aa861c446e4a2ed67278f4a5ce5
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979698"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>Conversão de configuração e opções de migração (AccessToSQL)
Para cada projeto do SSMA, você pode definir opções de nível de projeto. Essas opções especificam como os objetos são convertidos, como os dados são migrados e como os tipos de dados de origem são mapeados para tipos de dados de destino. Antes de converter objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure ou migrar os dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, verifique se as opções de configuração são adequadas para o projeto.  
  
## <a name="configuration-options-and-modes"></a>Modos e opções de configuração  
O SSMA tem quatro conjuntos de definições de configuração e quatro modos para definir essas configurações: padrão, Optimistic, completo e personalizado. O modo padrão é recomendado para a maioria dos usuários. Use o modo otimista para conversões simples. Use o modo completo se você quiser ver todas as mensagens. No modo personalizado, você deve definir as opções.  
  
As configurações são descritas na seção "Referência de Interface do usuário" desta documentação. Para obter mais informações sobre as configurações e como as configurações são aplicadas em cada modo, consulte os tópicos a seguir:  
  
-   [Configurações do projeto (conversão)](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [Configurações do projeto (migração)](http://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [Configurações do projeto (GUI)](http://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Configurações do projeto (mapeamento de tipo)](http://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [Configurações do projeto (SQL Azure)](http://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>Definir opções do projeto  
No SSMA, você pode configurar as configurações padrão para todos os projetos. Essas configurações são salvas no arquivo de configuração do SSMA e aplicadas a qualquer novo projeto criado por você.  
  
**Para definir opções de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações do projeto padrão**.  
  
2.  No **configurações de projeto padrão** caixa de diálogo, faça o seguinte:  
  
    -   Selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida / alterado de **versão de destino de migração** lista suspensa, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **Conversão ou migração ou SQL Azure**.  
  
        > [!NOTE]  
        > Opção do SQL Azure está disponível na **geral** guia somente se o tipo de projeto criado é do SQL Azure.  
  
    -   Para selecionar um modo predefinido, selecione **padrão**, **Optimistic**, ou **completo** no **modo** caixa suspensa.  
  
    -   Para especificar um modo personalizado, selecione **personalizado** na **modo** caixa, selecione uma opção no painel esquerdo, clique na configuração ou o valor no painel direito e, em seguida, selecione ou insira a nova configuração ou valor.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
Você também pode personalizar configurações para o projeto atual. Essas configurações são salvas no arquivo de projeto atual.  
  
**Para personalizar as configurações para o projeto atual**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações do projeto**.  
  
2.  No **configurações do projeto** caixa de diálogo, faça o seguinte:  
  
    -   Para selecionar um modo predefinido, selecione **padrão**, **Optimistic**, ou **completo** no **modo** caixa suspensa.  
  
    -   Para especificar um modo personalizado, selecione **personalizado** na **modo** caixa, selecione uma opção no painel esquerdo, clique na configuração ou o valor no painel direito e, em seguida, selecione ou insira a nova configuração ou valor.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento de tipos de dados de origem e destino, consulte [tipos de dados de destino e origem do mapeamento](http://msdn.microsoft.com/b362a075-16e7-423f-b63f-e1e9f02844a9)  
  
-   Para personalizar o mapeamento de bancos de dados de origem e destino, consulte [bancos de dados de destino e origem do mapeamento](http://msdn.microsoft.com/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
-   Caso contrário, você pode converter as definições de objeto de banco de dados do Access em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou definições de objeto do SQL Azure. Para obter mais informações, consulte [converter objetos de banco de dados do Access](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
