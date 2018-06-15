---
title: Função no SQLRemoveTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 495348c07ea707907f664358daea510951e7b208
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32918931"
---
# <a name="sqlremovetranslator-function"></a>Função no SQLRemoveTranslator
**Conformidade**  
 Versão introduzidas: ODBC 3.0  
  
 **Resumo**  
 **No SQLRemoveTranslator** remove informações sobre um conversor na seção Odbcinst.ini as informações de sistema e diminui a contagem de utilização de componente do tradutor por 1.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszTranslator*  
 [Entrada] O nome do tradutor como registrado na chave Odbcinst.ini as informações do sistema.  
  
 *lpdwUsageCount*  
 [Saída] A contagem de uso do tradutor depois que essa função foi chamada.  
  
## <a name="returns"></a>Retorna  
 A função retorna TRUE se for bem-sucedida, FALSO se ele falhar. Se não houver nenhuma entrada nas informações do sistema quando esta função é chamada, a função retornará FALSE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **no SQLRemoveTranslator** retorna FALSE, um tipo de  *\*pfErrorCode* valor pode ser obtido chamando **SQLInstallerError**. A seguinte tabela lista o  *\*pfErrorCode* valores que podem ser retornados por **SQLInstallerError** e explica cada uma no contexto dessa função.  
  
|*\*pfErrorCode*|Erro|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Erro geral de instalador|Ocorreu um erro para que nenhum erro específico do instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente não encontrado no registro|O instalador não foi possível remover as informações de conversor porque ele não existe no registro ou não pôde ser encontrado no registro.|  
|ODBC_ERROR_INVALID_NAME|Nome de driver ou conversor inválido|O *lpszTranslator* argumento era inválido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Não foi possível incrementar ou decrementar a contagem de uso do componente|Falha do instalador diminuir a contagem de uso do driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memória insuficiente|O instalador não pôde executar a função devido a uma falta de memória.|  
  
## <a name="comments"></a>Comentários  
 **No SQLRemoveTranslator** complementa o [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) função e atualizações o uso do componente contagem nas informações do sistema. Essa função deve ser chamada apenas de um aplicativo de instalação.  
  
 **No SQLRemoveTranslator** irá diminuir a contagem de uso do componente por 1. Se a contagem de uso do componente chegar a 0, a entrada de conversor nas informações do sistema será removida. A entrada de conversor está no seguinte local nas informações do sistema, sob o nome de conversor:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **No SQLRemoveTranslator** , na verdade, não remova os arquivos. O programa de chamada é responsável pela exclusão de arquivos e mantém a contagem de uso de arquivos. Somente quando a contagem de uso do componente e a contagem de uso do arquivo atingido zero é um arquivo excluído fisicamente. Alguns arquivos em um componente podem ser excluídos e outros não excluído, dependendo se os arquivos são usados por outros aplicativos que têm incrementado a contagem de uso de arquivos.  
  
 **No SQLRemoveTranslator** também é chamado como parte de um processo de atualização. Se um aplicativo detectar que ele tem que executar uma atualização e tiver instalado anteriormente o driver, o driver deve ser removido e reinstalado. **No SQLRemoveTranslator** primeiro deve ser chamado para diminuir a contagem de uso do componente e, em seguida, **SQLInstallTranslatorEx** deve ser chamado para incrementar a contagem de uso do componente. O programa de instalação do aplicativo fisicamente deve substituir os arquivos antigos com os novos arquivos. A contagem de uso de arquivo permanece o mesmo, e outros aplicativos que usam os arquivos da versão mais antigos agora usará a versão mais recente.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Instalando um conversor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
