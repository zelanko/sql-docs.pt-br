---
title: Método StartService (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- StartService Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartService method
ms.assetid: 83dfb6bd-dbd5-45d8-aad2-a11926317f91
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 67297de6badb15b493a5f17cbfe63bacc940a882
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73660835"
---
# <a name="startservice-method-sqlservice-class"></a>Método StartService (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Tenta colocar o serviço em seu estado iniciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.StartService()  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32 que especifica um dos seguintes estados de inicialização.  
  
 0  
 Sucesso. A solicitação foi aceita.  
  
 1  
 Sem suporte. A solicitação não terá suporte.  
  
 2  
 Acesso negado. O usuário não teve acesso apropriado.  
  
 3  
 Serviços Dependentes em Execução. O serviço não pode ser interrompido, porque outros serviços em execução dependem dele.  
  
 4  
 Controle de Serviço Inválido. O código de controle pedido não é válido ou é inaceitável para o serviço.  
  
 5  
 O Serviço Não Pode Aceitar o Controle. O código de controle solicitado não pode ser enviado ao serviço porque o estado do serviço (Win32_BaseService:State) é igual a 0, 1 ou 2.  
  
 6  
 Serviço Não Ativo. O serviço não foi iniciado.  
  
 7  
 Tempo Limite de Solicitação de Serviço. O serviço não respondeu à solicitação de início em um tempo oportuno.  
  
 8  
 Falha Desconhecida. Uma falha desconhecida ocorreu na inicialização do serviço.  
  
 9  
 Caminho Não Encontrado. O caminho do diretório para o executável de serviço não foi localizado.  
  
 10  
 Serviço Já em Execução. O serviço já está em execução.  
  
 11  
 Banco de Dados de Serviços Bloqueado. O banco de dados para adicionar um serviço novo está bloqueado.  
  
 12  
 Dependência de Serviço Excluída. Uma dependência da qual esse serviço depende foi removida do sistema.  
  
 13  
 Falha na Dependência do Serviço. O serviço não localizou o serviço necessário em um serviço dependente.  
  
 14  
 Serviço Desabilitado. O serviço foi desabilitado do sistema.  
  
 15  
 Falha de Logon de Serviço. O serviço não tem a autenticação correta para ser executado no sistema.  
  
 16  
 Serviço Marcado para Exclusão. O serviço está sendo removido do sistema.  
  
 17  
 Serviço sem-Thread. Não há nenhum thread de execução para o serviço.  
  
 18  
 Dependência Circular de Status. Há dependências circulares quando o serviço é iniciado.  
  
 19  
 Nome Duplicado de Status. Há um serviço em execução com o mesmo nome.  
  
 20  
 Nome Inválido de Status. Há caracteres que não são válido no nome do serviço.  
  
 21  
 Parâmetro Inválido do Status. Parâmetros que não são válidos foram transmitidos ao serviço.  
  
 22  
 Conta de Serviço Inválida de Status. A conta pela qual este serviço deve ser executado não é válida ou não possui as permissões para executar o serviço.  
  
 23  
 Serviço de Status Existe. O serviço existe no banco de dados de serviços disponível no sistema.  
  
 24  
 Serviço já em pausa. O serviço está pausado atualmente no sistema.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
