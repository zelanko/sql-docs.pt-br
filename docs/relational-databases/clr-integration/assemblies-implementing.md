---
title: Implementando assemblies | Microsoft Docs
description: Saiba como trabalhar com assemblies hospedados no SQL Server, incluindo como criar/modificar assemblies, remover ou habilitar/desabilitar assemblies e gerenciar versões.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d97ef8c7dfc617cb6cd56dbcc6d83e0540051d7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85695366"
---
# <a name="assemblies---implementing"></a>Assemblies – implementar
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico fornece informações sobre as seguintes áreas para ajudá-lo a implementar e trabalhar com assemblies no banco de dados:  
  
-   Criando assemblies  
  
-   Modificando assemblies  
  
-   Descartando, desabilitando e habilitando assemblies  
  
-   Gerenciando versões de assembly  
  
## <a name="creating-assemblies"></a>Criando Assemblies  
 Os assemblies são criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando o Assembly Assisted Editor. Além disso, a implantação de um projeto SQL Server no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra um assembly no banco de dados que foi especificado para o projeto. Para obter mais informações, consulte [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
  
 **Para criar um assembly usando o Transact-SQL**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
 **Para criar um assembly usando o SQL Server Management Studio**  
  
-   [Propriedades do assembly &#40;página Geral&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>Modificando assemblies  
 Os assemblies são modificados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução ALTER ASSEMBLY [!INCLUDE[tsql](../../includes/tsql-md.md)] ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando o Assembly Assisted Editor. Você pode modificar um assembly quando quiser fazer o seguinte:  
  
-   Altere a implementação do assembly carregando uma versão mais nova dos binários do assembly. Para obter mais informações, consulte [Gerenciando versões de assembly](#_managing) mais adiante neste tópico.  
  
-   Altere o conjunto de permissões do assembly. Para obter mais informações, confira [Criando assemblies](../../relational-databases/clr-integration/assemblies-designing.md).  
  
-   Altere a visibilidade do assembly. Assemblies visíveis estão disponíveis para consulta no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Assemblies não visíveis não estão disponíveis, mesmo se tiverem sido carregados no banco de dados. Por padrão, os assemblies carregados para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são visíveis.  
  
-   Adicione ou descarte um arquivo de depuração ou de origem associado ao assembly.  
  
 **Para modificar um assembly usando o Transact-SQL**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
 **Para modificar um assembly usando o SQL Server Management Studio**  
  
-   [Propriedades do assembly &#40;página Geral&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>Descartando, desabilitando e habilitando assemblies  
 Os assemblies são descartados usando a instrução DROP ASSEMBLY [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Para descartar um assembly usando o Transact-SQL**  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **Para descartar um assembly usando o SQL Server Management Studio**  
  
-   [Excluir Objetos](../../ssms/object/delete-objects.md)  
  
 Por padrão, todos os assemblies que são criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão desabilitados para execução. Você pode usar a opção **CLR Enabled** do procedimento armazenado do sistema **sp_configure** para desabilitar ou habilitar a execução de todos os assemblies que são carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Desabilitar a execução de assemblies impede que funções CLR (Common Language Runtime), procedimentos armazenados, gatilhos, agregações e tipos definidos pelo usuário sejam executados e interrompe os que estão sendo executados no momento. A desabilitação da execução do assembly não desabilita a capacidade de criar, alterar ou descartar assemblies. Para obter mais informações, consulte [opção de configuração de servidor CLR Enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md).  
  
 **Para desabilitar e habilitar a execução de assemblies**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
##  <a name="managing-assembly-versions"></a><a name="_managing"></a>Gerenciando versões de assembly  
 Quando um assembly é carregado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o assembly é armazenado e gerenciado dentro dos catálogos do sistema de banco de dados. Todas as alterações feitas na definição do assembly no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] devem ser propagadas para o assembly armazenado no catálogo de banco de dados.  
  
 Quando for preciso modificar um assembly, você deverá emitir uma instrução ALTER ASSEMBLY para atualizar o assembly no banco de dados. Isso atualizará o assembly até a última cópia de módulos do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que contenha sua implementação.  
  
 A cláusula WITH UNCHECKED DATA da instrução ALTER ASSEMBLY instrui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para atualizar até mesmo os assemblies dos quais os dados persistentes no banco de dados sejam dependentes. Especificamente, você deve especificar WITH UNCHECKED DATA se qualquer uma dessas opções existir:  
  
-   Colunas computadas persistentes que referenciem métodos no assembly, seja direta ou indiretamente, através de funções ou métodos [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   As colunas de um tipo de dado CLR definido pelo usuário que dependem do assembly e o tipo implementa um formato de serialização **UserDefined** (não **nativo**).  
  
> [!CAUTION]  
>  Se WITH UNCHECKED DATA não for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentará impedir que ALTER ASSEMBLY seja executada se a nova versão do assembly afetar dados existentes em tabelas, índices ou outros locais persistentes. Porém, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não garante que colunas computadas, índices, exibições indexadas ou expressões sejam consistentes com as rotinas e tipos subjacentes quando o assembly CLR for atualizado. Tenha cuidado ao executar ALTER ASSEMBLY, para ter certeza de que não haja nenhuma desigualdade entre o resultado de uma expressão e um valor que é baseado naquela expressão armazenado no assembly.  
  
 Somente os membros do **db_owner** e **db_ddlowner** função de banco de dados fixa podem executar a execução de ALTER assembly usando a cláusula WITH desmarcated Data.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publica uma mensagem no log de eventos de aplicativos do Windows informando que o assembly foi modificado com dados não verificados nas tabelas. Em seguida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] marca qualquer tabela que contenha dados dependentes do assembly como tendo dados não verificados. A coluna **has_unchecked_assembly_data** da exibição de catálogo **Sys. Tables** contém o valor 1 para tabelas que contêm dados desmarcados e 0 para tabelas sem dados desmarcados.  
  
 Para resolver a integridade dos dados desmarcados, execute DBCC CHECKDB com EXTENDED_LOGICAL_CHECKS em cada tabela que tem dados desmarcados. Se o DBCC CHECKDB com EXTENDED_LOGICAL_CHECKS falhar, você deverá excluir as linhas da tabela que não são válidas ou modificar o código do assembly para resolver problemas e, em seguida, emitir instruções ALTER ASSEMBLY adicionais.  
  
 ALTER ASSEMBLY altera a versão do assembly. A cultura e o token de chave pública do assembly permanecem os mesmos. SQL Server não permite registrar versões diferentes de um assembly com o mesmo nome, cultura e chave pública.  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>Interações com a política de computadores para associação de versões  
 Se as referências a assemblies armazenadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forem redirecionadas a versões específicas usando política de publicador ou política de administrador de computadores, você deve agir de uma das seguintes maneiras:  
  
-   Verificar se a nova versão para a qual esse redirecionamento é feito está no banco de dados.  
  
-   Modificar qualquer instrução dos arquivos de política externa do computador ou de política de publicador para ter certeza de que fazem referência à versão específica que está no banco de dados.  
  
 Caso contrário, uma tentativa para carregar uma nova versão de assembly à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] falhará.  
  
 **Para atualizar a versão de um assembly**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Assemblies &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Obtendo informações sobre assemblies](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
