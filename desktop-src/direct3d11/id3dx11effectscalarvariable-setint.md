---
title: ID3DX11EffectScalarVariable SetInt method (D3dx11effect.h)
description: Set an integer variable.
ms.assetid: 614284be-8f70-4d7e-b797-b67e813615ab
keywords:
- SetInt method Direct3D 11
- SetInt method Direct3D 11 , ID3DX11EffectScalarVariable interface
- ID3DX11EffectScalarVariable interface Direct3D 11 , SetInt method
topic_type:
- apiref
api_name:
- ID3DX11EffectScalarVariable.SetInt
api_location:
- N/A
- N/A.dll
api_type:
- COM
ms.topic: reference
ms.date: 05/31/2018
---

# ID3DX11EffectScalarVariable::SetInt method

Set an integer variable.

## Syntax


```C++
HRESULT SetInt(
   int Value
);
```



## Parameters

<dl> <dt>

*Value* 
</dt> <dd>

Type: **[**int**](https://docs.microsoft.com/windows/desktop/WinProg/windows-data-types)**

A pointer to the variable.

</dd> </dl>

## Return value

Type: **[**HRESULT**](https://msdn.microsoft.com/library/Bb401631(v=MSDN.10).aspx)**

Returns one of the following [Direct3D 11 Return Codes](d3d11-graphics-reference-returnvalues.md).

## Remarks

> [!Note]  
> The DirectX SDK does not supply any compiled binaries for effects. You must use Effects 11 source to build your effects-type application. For more information about using Effects 11 source, see [Differences Between Effects 10 and Effects 11](d3d11-graphics-programming-guide-effects-differences.md).

 

## Requirements



|                    |                                                                                                                                              |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Header<br/>  | <dl> <dt>D3dx11effect.h</dt> </dl>                                                    |
| Library<br/> | <dl> <dt>N/A (An Effects 11 library is available online as shared source.)</dt> </dl> |



## See also

<dl> <dt>

[ID3DX11EffectScalarVariable](id3dx11effectscalarvariable.md)
</dt> </dl>

 

 





