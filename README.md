# NextJS-API-Update-Delete-Operation

### Update Operation
![](https://imgur.com/jlinOLI.png)

```bash
import { NextRequest, NextResponse } from "next/server";
import prisma from "@/lib/prisma";


export async function PUT(request: NextRequest) {
    try {
        
        const {searchParams} = new URL(request.url);
        const id = searchParams.get('id');
        const jsonBody = await request.json();

        if (!id) {
            return NextResponse.json(
                {status: "Employee id is required!"},
                {status: 400}
            )
        }

        const updateEmployeeData = await prisma.employee.update({
            where: {id:id},
            data: jsonBody,
        })

        return NextResponse.json(
            {status: "success", data: updateEmployeeData},
            {status: 200}
        )
    } catch (error) {
        console.log("Employee Update error:", error)
        return NextResponse.json(
            {status: "Failed", message: "Employee Data Update Error"},
            {status: 500}
        )
    }
}
```
---
