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
                {status: "Failed", message: "Missing 'id' query parameter"},
                {status: 400}
            )
        }

        const updateEmployeeData = await prisma.employee.update({
            where: { id },
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

### Delete operation
![](https://imgur.com/QL49kkI.png)

```bash
import prisma from "@/lib/prisma";
import { NextRequest, NextResponse } from "next/server";


export async function DELETE(request: NextRequest) {
    try {
        
        const {searchParams} = new URL(request.url);
        const id = searchParams.get("id");

        if (!id) {
            return NextResponse.json(
                {status: "failed", message: "id is required"},
                {status: 400}
            )
        }

        const employeeIdDelete = await prisma.employee.delete({
            where: {id}
        })

        return NextResponse.json(
            {status: "success", message: "Deleted Employee record", data: employeeIdDelete},
            {status: 200}
        )
    } catch (error) {
        console.log("Delete Employee operation error:", error)
        return NextResponse.json(
            {status: "failed", message: "Delete operation failed!"},
            {status: 500}
        )
    }
}
```
---
