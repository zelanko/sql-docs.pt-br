---
title: Propriedades do SQL Server (guia Parâmetros de Inicialização)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 16942624-5374-446c-8de4-ee6ed34d6e94
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 2d5a4c5cb279cb4cfd4bbe1baa63f89dc1289436
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75306769"
---
# <a name="sql-server-properties-startup-parameters-tab"></a>Propriedades do SQL Server (guia Parâmetros de Inicialização)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Use esta caixa de diálogo para adicionar ou remover parâmetros de inicialização do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Os parâmetros de inicialização podem ter um grande efeito no desempenho do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Antes de adicionar ou alterar os parâmetros de inicialização, consulte o tópico "Usando as opções de inicialização do Serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] " nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Especificar um parâmetro de inicialização**  
 Para adicionar um parâmetro, digite o parâmetro e clique em **Adicionar**.  
  
 Para modificar um dos parâmetros necessários, selecione o parâmetro na caixa **Parâmetros existentes** , altere os valores da caixa **Especificar um parâmetro de inicialização** e clique em **Atualizar**.  
  
 **Parâmetros existentes**  
 Para remover um parâmetro, selecione um parâmetro e clique em **Remover**.  
  
## <a name="parameter-format"></a>Formato do parâmetro  
 Não insira um separador entre parâmetros. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager adiciona o separador automaticamente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager impõe os seguintes requisitos de parâmetros.  
  
-   Espaços à direita e à esquerda são cortados de qualquer parâmetro de inicialização.  
  
-   Todos os parâmetros de inicialização começam com um - (traço) e o segundo valor é uma letra.  
  
## <a name="required-parameters"></a>Parâmetros obrigatórios  
 As seguintes parâmetros são necessários. Eles podem ser alterados, mas não poder ser removidos.  
  
-   -d é o caminho do arquivo **master.mdf** (o arquivo de dados do banco de dados mestre).  
  
-   -l é o caminho do arquivo **master.ldf** (o arquivo de log do banco de dados mestre).  
  
-   -e é o caminho dos arquivos de log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!CAUTION]  
>  Se os parâmetros de caminho de arquivo estiverem incorretos, talvez o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não possa ser iniciado.  
  
 Para obter mais informações sobre como mover o banco de dados mestre, consulte o tópico "Movendo bancos de dados do sistema" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="optional-parameters"></a>Parâmetros opcionais  
 Todos os parâmetros de inicialização com suporte são descritos no tópico "Usando as opções de inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ", nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Um parâmetro de inicialização -T*trace#* indica que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser iniciada com um sinalizador de rastreamento (*trace#* ) em vigor. São usados sinalizadores de rastreamento para iniciar o servidor com comportamento fora do padrão. Para obter mais informações sobre sinalizadores de rastreamento, confira o tópico "Sinalizadores de rastreamento ([!INCLUDE[tsql](../../includes/tsql-md.md)])" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!CAUTION]  
>  Talvez você veja parâmetros de inicialização e sinalizadores de rastreamento adicionais não documentados na Internet. Os parâmetros de inicialização e os indicadores de rastreamento não documentados são criados para resolver problemas ou para forçar determinas condições necessárias para testes. O uso de parâmetros de inicialização não documentados pode ter resultados inesperados. Não use parâmetros não documentados a não ser quando direcionado pelos Serviços de Atendimento ao Cliente da Microsoft.  
  
 A lista a seguir descreve alguns parâmetros opcionais comuns.  
  
|Parâmetro|Descrição breve|  
|---------------|-----------------------|  
|-M|Inicia uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de usuário único.|  
|-T1204|Retorna os recursos e tipos de bloqueios que participam de um deadlock e também o comando atual afetado.|  
|-T1224|Desabilita o escalonamento de bloqueios com base no número de bloqueios.|  
|-T3608|Impede que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicie ou recupere automaticamente qualquer banco de dados, exceto o banco de dados mestre.|  
|-T7806|Habilita uma conexão de administrador dedicada (DAC) no [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].|  
  
> [!CAUTION]  
>  Alguns parâmetros opcionais podem alterar o comportamento do servidor e afetar o desempenho.  
  
## <a name="permissions"></a>Permissões  
 O uso desta página é restrito a usuários que podem alterar as entradas relacionadas no Registro. Isso inclui os seguintes usuários.  
  
-   Membros do grupo Administradores local.  
  
-   A conta de domínio usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver configurado para ser executado em uma conta de domínio.  
  
## <a name="books-online-references"></a>Referências dos Manuais Online  
 Para obter mais informações sobre os parâmetros de inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira "Como configurar as opções de inicialização do servidor (Configuration Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
