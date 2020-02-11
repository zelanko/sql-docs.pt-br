---
title: Considerações para usar servidores de teste | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- overhead [Database Engine Tuning Advisor]
- tuning overhead [SQL Server]
- reducing production server tuning load
- Database Engine Tuning Advisor [SQL Server], test servers
- xp_msver
- test servers [Database Engine Tuning Advisor]
- production servers [SQL Server]
- offload tuning overhead [SQL Server]
ms.assetid: 94e6c3e5-1f09-4616-9da2-4e44d066d494
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c1ed99e6ee3ef6385e6041044e9b2cb829b1b3ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63151139"
---
# <a name="considerations-for-using-test-servers"></a>Considerações para usar servidores de teste
  Usar um servidor de teste para ajustar um banco de dados em um servidor de produção é uma vantagem importante do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Usando esse recurso, você pode descarregar a sobrecarga de ajuste em um servidor de teste sem copiar os dados reais no servidor de teste do servidor de produção.  
  
> [!NOTE]  
>  O recurso de ajuste do servidor de teste não é suportado na interface gráfica de usuário do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 Para usar esse recurso com sucesso, verifique as considerações listadas nas seções seguintes.  
  
## <a name="setting-up-the-test-serverproduction-server-environment"></a>Preparando o ambiente do servidor de teste/servidor de produção  
  
-   O usuário que deseje usar um servidor de teste para ajustar um banco de dados em um servidor de produção deve existir em ambos os servidores ou este cenário não funcionará.  
  
-   O procedimento armazenado estendido, **xp_msver**, deve ser habilitado para usar o cenário de servidor de teste/servidor de produção. [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa esse procedimento armazenado estendido para buscar o número de processadores e a memória disponível do servidor de produção a ser usado durante a otimização do servidor de teste. Se **xp_msver** não for habilitado, o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] assumirá as características de hardware do computador no qual o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] está sendo executado. Se as características de hardware do computador onde Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] está sendo executado não estão disponíveis, são assumidos um processador e 1024 MB (megabytes) de memória. Esse procedimento armazenado estendido é ativado por padrão quando você instala o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Configuração da Área de Superfície](../security/surface-area-configuration.md) e [xp_msver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/xp-msver-transact-sql).  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] espera que as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sejam iguais no servidor de teste e no servidor de produção. Se houver duas edições diferentes, a edição no servidor de teste terá precedência. Por exemplo, se o servidor de teste estiver executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard, o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não incluirá exibições indexadas, particionamentos e operações online em suas recomendações mesmo que o servidor de produção esteja executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise.  
  
## <a name="about-test-serverproduction-server-behavior"></a>Sobre o comportamento do servidor teste/servidor de produção  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] leva em conta as diferenças de hardware entre o servidor de produção e de teste ao criar recomendações. A recomendação é a mesma, como se o ajuste tivesse sido feito apenas no servidor de produção.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode impor alguma carga no servidor de produção para reunir metadados, assim como para a criação de estatísticas necessárias para o ajuste.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] não copia dados reais do servidor de produção para o servidor de teste. Apenas copia os metadados dos bancos de dados e as estatísticas necessárias.  
  
-   Todas as informações da sessão são armazenadas no **msdb** do servidor de produção. Isso permite explorar qualquer servidor de teste disponível para o ajuste e as informações sobre todas as sessões estão disponíveis em um só lugar (o servidor de produção).  
  
## <a name="issues-related-to-the-shell-database"></a>Problemas relacionados ao banco de dados shell  
  
-   Depois de ajustar, o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deverá remover quaisquer metadados que criou no servidor de teste durante o processo de ajuste. Isso inclui o banco de dados shell. Se você estiver executando uma série de sessões de ajuste com os mesmos servidores de produção e de teste, poderá desejar reter esse banco de dados shell para economizar tempo. No arquivo de entrada XML, especifique o subelemento **RetainShellDB** com os outros subelementos no elemento pai **TuningOptions** . Usar essas opções faz o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] reter o banco de dados shell. Para obter mais informações, veja [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](database-engine-tuning-advisor.md).  
  
-   Os bancos de dados shell poderão ser deixados no servidor de teste após uma sessão bem-sucedida de ajuste do servidor de teste/servidor de produção mesmo que você não tenha especificado o subelemento **RetainShellDB** . Esses bancos de dados de shell não desejados podem interferir com sessões de ajuste subsequentes e podem ser cancelados antes de executar outra sessão de ajuste do servidor de teste/servidor de produção. Além disso, se uma sessão de ajuste fechar inesperadamente, os bancos de dados de shell poderão ser deixados no servidor de teste e os objetos dentro desses bancos de dados deixados no servidor de teste. Você também deverá excluir esses bancos de dados e objetos antes de iniciar uma nova sessão de ajuste do servidor de teste/servidor de produção.  
  
## <a name="issues-related-to-the-tuning-process"></a>Problemas relacionados ao processo de ajuste  
  
-   O usuário deve verificar o log de ajuste para ajustar erros resultantes de diferenças entre os servidores de produção e de teste, e para os erros resultantes da cópia de metadados do servidor de produção para o de teste. Por exemplo, um logon de usuário pode não existir no servidor de teste. Se um logon de usuário não existir no servidor de teste, esses eventos na carga de trabalho emitidos por esse logon de usuário poderão não ser ajustáveis. Use o GUI do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para exibir o log de ajuste. Para obter mais informações, veja [Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)  
  
-   Se o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não puder ajustar muitos eventos porque os objetos estão ausentes no banco de dados shell que o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria no servidor de teste, o usuário deve verificar o log de ajuste. Os eventos que não podem ser ajustados são listados no log. Para ajustar o banco de dados com êxito no servidor de teste, o usuário deve criar os objetos ausentes no banco de dados shell e então iniciar uma nova sessão de ajuste.  
  
-   Se um banco de dados com o mesmo nome já existir no servidor de teste, o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não copiará os metadados, mas continuará o ajuste e reunirá as estatísticas se for necessário. Isso é útil se o usuário já criou um banco de dados no servidor de teste e copiou os metadados apropriados antes de chamar o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
-   Se a opção DATE_CORRELATION_OPTIMIZATION for ativada para um banco de dados no servidor de produção, os metadados e os dados associados com essa opção não serão totalmente incluídos no script durante o ajuste do servidor de teste. Quando o ajuste é executado para um cenário de servidor de teste/servidor de produção, os problemas seguintes podem ser aplicáveis:  
  
    -   Os usuários podem ter planos de consulta diferentes nos servidores para consultas que usam a opção DATE_CORRELATION_OPTIMIZATION.  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] O Orientador de Otimização poderá sugerir a remoção das exibições indexadas que impõem a opção DATE_CORRELATION_OPTIMIZATION no script de recomendação.  
  
     Por isso, você pode querer ignorar qualquer recomendação que o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] faça sobre as exibições indexadas que mantêm estatísticas de correlação, porque o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] conhece os seus custos mas não os seus benefícios. [!INCLUDE[ssDE](../../includes/ssde-md.md)] O Orientador de Otimização poderá não recomendar a seleção de alguns índices, como índices clusterizados em colunas **datetime** , que podem ser benéficos quando DATE_CORRELATION_OPTIMIZATION é habilitado.  
  
     Para determinar se uma exibição é baseada em estatísticas de correlação, selecione a coluna **is_date_correlation_view** da exibição de catálogo [sys.views](/sql/relational-databases/system-catalog-views/sys-views-transact-sql) .  
  
  
