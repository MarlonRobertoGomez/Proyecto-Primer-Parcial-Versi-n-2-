# Proyecto-Primer-Parcial-Versi-n-2-
Tarea de Programacion II
using System;
using System.Collections.Generic;
using System.Linq;

namespace GestionSistema
{
    class Program
    {
        
        public class Producto
        {
            public int Codigo { get; set; }
            public string Nombre { get; set; }
            public decimal Precio { get; set; }
            public int Stock { get; set; }
        }

        public class Cliente
        {
            public string TipoDocumento { get; set; }
            public string Documento { get; set; }
            public string Nombre { get; set; }
            public DateTime FechaIngreso { get; set; }
            public string Categoria { get; set; }
        }

        public class Empleado
        {
            public int Codigo { get; set; }
            public string Nombre { get; set; }
            public DateTime FechaIngreso { get; set; }
            public string Puesto { get; set; }
            public string TipoDocumento { get; set; }
            public string Documento { get; set; }
        }

        public class Factura
        {
            public int Id { get; set; }
            public DateTime FechaIngreso { get; set; }
            public string IdCliente { get; set; }
            public int IdEmpleado { get; set; }
            public decimal SubTotal { get; set; }
            public decimal ISV { get; set; }
            public decimal Descuento { get; set; }
            public decimal TotalPagar => SubTotal + ISV - Descuento;
            public List<DetalleFactura> Detalles { get; set; } = new List<DetalleFactura>();
        }

        public class DetalleFactura
        {
            public int IdFactura { get; set; }
            public int IdProducto { get; set; }
            public string Nombre { get; set; }
            public decimal Precio { get; set; }
            public int CantidadLlevada { get; set; }
            public decimal SubTotal => Precio * CantidadLlevada;
        }

        static void Main(string[] args)
        {
            List<Producto> productos = new List<Producto>();
            List<Cliente> clientes = new List<Cliente>();
            List<Empleado> empleados = new List<Empleado>();
            List<Factura> facturas = new List<Factura>();

            while (true)
            {
                Console.Clear();
                Console.WriteLine("Menú:");
                Console.WriteLine("a. Productos");
                Console.WriteLine("b. Clientes");
                Console.WriteLine("c. Empleados");
                Console.WriteLine("d. Facturas");
                Console.WriteLine("e. Histórico de Facturas");
                Console.WriteLine("f. Salir");
                Console.Write("Seleccione una opción: ");
                char opcion = Console.ReadKey().KeyChar;
                Console.WriteLine();

                switch (opcion)
                {
                    case 'a':
                        AgregarProducto(productos);
                        break;
                    case 'b':
                        AgregarCliente(clientes);
                        break;
                    case 'c':
                        AgregarEmpleado(empleados);
                        break;
                    case 'd':
                        AgregarFactura(facturas, productos, clientes, empleados);
                        break;
                    case 'e':
                        MostrarHistoricoFacturas(facturas);
                        break;
                    case 'f':
                        return;
                    default:
                        Console.WriteLine("Opción no válida. Intente de nuevo.");
                        break;
                }
            }
        }

        static void AgregarProducto(List<Producto> productos)
        {
            try
            {
                Producto nuevoProducto = new Producto();
                Console.Write("Ingrese el Código del producto: ");
                nuevoProducto.Codigo = int.Parse(Console.ReadLine());
                Console.Write("Ingrese el Nombre del producto: ");
                nuevoProducto.Nombre = Console.ReadLine();
                Console.Write("Ingrese el Precio del producto: ");
                nuevoProducto.Precio = decimal.Parse(Console.ReadLine());
                Console.Write("Ingrese el Stock del producto: ");
                nuevoProducto.Stock = int.Parse(Console.ReadLine());

                productos.Add(nuevoProducto);
                Console.WriteLine("Producto agregado con éxito.");
            }
            catch (FormatException)
            {
                Console.WriteLine("Error: Formato de entrada no válido.");
            }
            Console.ReadLine();
        }

        static void AgregarCliente(List<Cliente> clientes)
        {
            try
            {
                Cliente nuevoCliente = new Cliente();
                Console.Write("Ingrese el Tipo de Documento: ");
                nuevoCliente.TipoDocumento = Console.ReadLine();
                Console.Write("Ingrese el Documento: ");
                nuevoCliente.Documento = Console.ReadLine();
                Console.Write("Ingrese el Nombre: ");
                nuevoCliente.Nombre = Console.ReadLine();
                Console.Write("Ingrese la Fecha de Ingreso (yyyy-mm-dd): ");
                nuevoCliente.FechaIngreso = DateTime.Parse(Console.ReadLine());
                Console.Write("Ingrese la Categoría: ");
                nuevoCliente.Categoria = Console.ReadLine();

                clientes.Add(nuevoCliente);
                Console.WriteLine("Cliente agregado con éxito.");
            }
            catch (FormatException)
            {
                Console.WriteLine("Error: Formato de entrada no válido.");
            }
            Console.ReadLine();
        }

        static void AgregarEmpleado(List<Empleado> empleados)
        {
            try
            {
                Empleado nuevoEmpleado = new Empleado();
                Console.Write("Ingrese el Código: ");
                nuevoEmpleado.Codigo = int.Parse(Console.ReadLine());
                Console.Write("Ingrese el Nombre: ");
                nuevoEmpleado.Nombre = Console.ReadLine();
                Console.Write("Ingrese la Fecha de Ingreso (yyyy-mm-dd): ");
                nuevoEmpleado.FechaIngreso = DateTime.Parse(Console.ReadLine());
                Console.Write("Ingrese el Puesto: ");
                nuevoEmpleado.Puesto = Console.ReadLine();
                Console.Write("Ingrese el Tipo de Documento: ");
                nuevoEmpleado.TipoDocumento = Console.ReadLine();
                Console.Write("Ingrese el Documento: ");
                nuevoEmpleado.Documento = Console.ReadLine();

                empleados.Add(nuevoEmpleado);
                Console.WriteLine("Empleado agregado con éxito.");
            }
            catch (FormatException)
            {
                Console.WriteLine("Error: Formato de entrada no válido.");
            }
            Console.ReadLine();
        }

        static void AgregarFactura(List<Factura> facturas, List<Producto> productos, List<Cliente> clientes, List<Empleado> empleados)
        {
            try
            {
                Factura nuevaFactura = new Factura();
                Console.Write("Ingrese el Id de la Factura: ");
                nuevaFactura.Id = int.Parse(Console.ReadLine());
                Console.Write("Ingrese la Fecha de Ingreso (yyyy-mm-dd): ");
                nuevaFactura.FechaIngreso = DateTime.Parse(Console.ReadLine());

                Console.Write("Ingrese el Id del Cliente: ");
                nuevaFactura.IdCliente = Console.ReadLine();
                Console.Write("Ingrese el Id del Empleado: ");
                nuevaFactura.IdEmpleado = int.Parse(Console.ReadLine());

                Console.Write("Ingrese el SubTotal: ");
                nuevaFactura.SubTotal = decimal.Parse(Console.ReadLine());
                Console.Write("Ingrese el ISV: ");
                nuevaFactura.ISV = decimal.Parse(Console.ReadLine());
                Console.Write("Ingrese el Descuento: ");
                nuevaFactura.Descuento = decimal.Parse(Console.ReadLine());

                // Agregar detalles de la factura
                Console.Write("¿Desea agregar detalles a la factura? (s/n): ");
                char respuesta = Console.ReadKey().KeyChar;
                Console.WriteLine();
                while (respuesta == 's')
                {
                    DetalleFactura detalle = new DetalleFactura();
                    Console.Write("Ingrese el Id del Producto: ");
                    detalle.IdProducto = int.Parse(Console.ReadLine());
                    var producto = productos.FirstOrDefault(p => p.Codigo == detalle.IdProducto);
                    if (producto == null)
                    {
                        Console.WriteLine("Producto no encontrado.");
                        continue;
                    }
                    detalle.Nombre = producto.Nombre;
                    detalle.Precio = producto.Precio;

                    Console.Write("Ingrese la Cantidad Llevada: ");
                    detalle.CantidadLlevada = int.Parse(Console.ReadLine());

                    nuevaFactura.Detalles.Add(detalle);
                    Console.Write("¿Desea agregar otro detalle? (s/n): ");
                    respuesta = Console.ReadKey().KeyChar;
                    Console.WriteLine();
                }

                facturas.Add(nuevaFactura);
                Console.WriteLine("Factura agregada con éxito.");
            }
            catch (FormatException)
            {
                Console.WriteLine("Error: Formato de entrada no válido.");
            }
            Console.ReadLine();
        }

        static void MostrarHistoricoFacturas(List<Factura> facturas)
        {
            Console.WriteLine("Histórico de Facturas:");
            foreach (var factura in facturas)
            {
                Console.WriteLine($"Id: {factura.Id}, Fecha: {factura.FechaIngreso}, Total a Pagar: {factura.TotalPagar}");
                foreach (var detalle in factura.Detalles)
                {
                    Console.WriteLine($"   Detalle - Id Producto: {detalle.IdProducto}, Nombre: {detalle.Nombre}, Cantidad: {detalle.CantidadLlevada}, SubTotal: {detalle.SubTotal}");
                }
            }
            Console.ReadLine();
        
        
        }
    }
}
using System;
using System.Collections.Generic;


namespace GestionSistema
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
        }

        private void InitializeComponent()
        {
            throw new NotImplementedException();
        }

        private void btnProductos_Click(object sender, EventArgs e)
        {
            ProductosForm productosForm = new ProductosForm();
            productosForm.Show();
        }

        private void btnClientes_Click(object sender, EventArgs e)
        {
            ClientesForm clientesForm = new ClientesForm();
            clientesForm.Show();
        }
    }

    public class Producto
    {
        public int Codigo { get; set; }
        public string Nombre { get; set; }
        public decimal Precio { get; set; }
        public int Stock { get; set; }
    }

    public class Cliente
    {
        public string TipoDocumento { get; set; }
        public string Documento { get; set; }
        public string Nombre { get; set; }
        public DateTime FechaIngreso { get; set; }
        public string Categoria { get; set; }
    }

    public partial class ProductosForm : Form
    {
        private List<Producto> productos = new List<Producto>();

        public object MessageBox { get; private set; }

        public ProductosForm()
        {
            InitializeComponent();
        }

        private void InitializeComponent()
        {
            throw new NotImplementedException();
        }

        private void btnAgregarProducto_Click(object sender, EventArgs e)
        {
            Producto nuevoProducto = new Producto()
            {
                Codigo = int.Parse(txtCodigo.Text),
                Nombre = txtNombre.Text,
                Precio = decimal.Parse(txtPrecio.Text),
                Stock = int.Parse(txtStock.Text)
            };

            productos.Add(nuevoProducto);
            MessageBox.Show("Producto agregado correctamente.");
        }

        internal void Show()
        {
            throw new NotImplementedException();
        }
    }

    public partial class ClientesForm : Form
    {
        private List<Cliente> clientes = new List<Cliente>();

        public ClientesForm()
        {
            InitializeComponent();
        }

        private void InitializeComponent()
        {
            throw new NotImplementedException();
        }

        private void btnAgregarCliente_Click(object sender, EventArgs e)
        {
            Cliente nuevoCliente = new Cliente()
            {
                TipoDocumento = txtTipoDocumento.Text,
                Documento = txtDocumento.Text,
                Nombre = txtNombre.Text,
                FechaIngreso = DateTime.Parse(txtFechaIngreso.Text),
                Categoria = txtCategoria.Text
            };

            clientes.Add(nuevoCliente);
            MessageBox.Show("Cliente agregado correctamente.");
        }

        internal void Show()
        {
            throw new NotImplementedException();
        }
    }
}
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace GestionEmpleados
{
    public partial class Form1 : Form
    {
        private List<Empleado> listaEmpleados = new List<Empleado>();

        public Form1()
        {
            InitializeComponent();
        }

        private void btnAgregar_Click(object sender, EventArgs e)
        {
            try
            {
                Empleado nuevoEmpleado = new Empleado
                {
                    Codigo = int.Parse(txtCodigo.Text),
                    Nombre = txtNombre.Text,
                    FechaIngreso = dtpFechaIngreso.Value,
                    Puesto = txtPuesto.Text,
                    TipoDocumento = cmbTipoDocumento.SelectedItem.ToString(),
                    Documento = txtDocumento.Text
                };

                listaEmpleados.Add(nuevoEmpleado);
                ActualizarLista();
                LimpiarCampos();
            }
            catch (Exception ex)
            {
                MessageBox.Show("Error al agregar empleado: " + ex.Message);
            }
        }

        private void ActualizarLista()
        {
            dgvEmpleados.DataSource = null;
            dgvEmpleados.DataSource = listaEmpleados;
        }

        private void LimpiarCampos()
        {
            txtCodigo.Clear();
            txtNombre.Clear();
            txtPuesto.Clear();
            txtDocumento.Clear();
            cmbTipoDocumento.SelectedIndex = -1;
        }
    }
}
using System;
using System.Data;
using System.Linq;
using System.Windows.Forms;

namespace FacturacionApp
{
    public partial class FrmFacturas : Form
    {
        FacturacionEntities db = new FacturacionEntities();

        public FrmFacturas()
        {
            InitializeComponent();
        }

        private void FrmFacturas_Load(object sender, EventArgs e)
        {
            CargarFacturas();
        }

        private void CargarFacturas()
        {
            dgvFacturas.DataSource = db.Factura
                .Select(f => new { 
                    f.IdFactura, 
                    f.FechaIngreso, 
                    f.IdCliente, 
                    f.IdEmpleado, 
                    f.SubTotal, 
                    f.ISV, 
                    f.Descuento, 
                    f.TotalPagar 
                }).ToList();
        }

        private void dgvFacturas_SelectionChanged(object sender, EventArgs e)
        {
            if (dgvFacturas.SelectedRows.Count > 0)
            {
                int idFactura = Convert.ToInt32(dgvFacturas.SelectedRows[0].Cells["IdFactura"].Value);
                CargarDetalles(idFactura);
            }
        }

        private void CargarDetalles(int idFactura)
        {
            dgvDetalles.DataSource = db.DetalleFactura
                .Where(d => d.IdFactura == idFactura)
                .Select(d => new { 
                    d.IdDetalle, 
                    d.IdProducto, 
                    d.Nombre, 
                    d.Precio, 
                    d.CantidadLlevada, 
                    d.SubTotal 
                }).ToList();
        }

        private void btnAgregarFactura_Click(object sender, EventArgs e)
        {
            Factura nuevaFactura = new Factura()
            {
                FechaIngreso = DateTime.Now,
                IdCliente = 1, // Puedes cambiarlo dinámicamente
                IdEmpleado = 1, // Puedes cambiarlo dinámicamente
                SubTotal = 0,
                ISV = 0,
                Descuento = 0,
                TotalPagar = 0
            };

            db.Factura.Add(nuevaFactura);
            db.SaveChanges();
            CargarFacturas();
        }

        private void btnAgregarDetalle_Click(object sender, EventArgs e)
        {
            if (dgvFacturas.SelectedRows.Count > 0)
            {
                int idFactura = Convert.ToInt32(dgvFacturas.SelectedRows[0].Cells["IdFactura"].Value);

                DetalleFactura nuevoDetalle = new DetalleFactura()
                {
                    IdFactura = idFactura,
                    IdProducto = 1, // Puedes cambiarlo dinámicamente
                    Nombre = "Producto de ejemplo",
                    Precio = 100,
                    CantidadLlevada = 1,
                    SubTotal = 100
                };

                db.DetalleFactura.Add(nuevoDetalle);
                db.SaveChanges();
                CargarDetalles(idFactura);
            }
        }

        private void btnEliminarFactura_Click(object sender, EventArgs e)
        {
            if (dgvFacturas.SelectedRows.Count > 0)
            {
                int idFactura = Convert.ToInt32(dgvFacturas.SelectedRows[0].Cells["IdFactura"].Value);
                Factura factura = db.Factura.Find(idFactura);

            if (factura != null)
            {
                db.Factura.Remove(factura);
                db.SaveChanges();
                CargarFacturas();
            }
        }
    }
    
    private void btnEliminarDetalle_Click(object sender, EventArgs e)
    {
        if (dgvDetalles.SelectedRows.Count > 0)
        {
            int idDetalle = Convert.ToInt32(dgvDetalles.SelectedRows[0].Cells["IdDetalle"].Value);
            DetalleFactura detalle = db.DetalleFactura.Find(idDetalle);

            if (detalle != null)
            {
                db.DetalleFactura.Remove(detalle);
                db.SaveChanges();
                CargarDetalles(detalle.IdFactura);
            }
        }
    }
    using System;
using System.Linq;
using System.Windows.Forms;

public partial class Form1 : Form
{
    private MiDbContext db = new MiDbContext(); // Contexto de la base de datos

    public Form1()
    {
        InitializeComponent();
    }

    private void btnBuscar_Click(object sender, EventArgs e)
    {
        // Validar entrada del usuario
        if (!int.TryParse(txtIdFactura.Text, out int idFactura))
        {
            MessageBox.Show("Ingrese un ID válido.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Warning);
            return;
        }

        // Buscar la factura en la base de datos usando LINQ
        var factura = db.Facturas
                        .Where(f => f.IdFactura == idFactura)
                        .Select(f => new
                        {
                            f.IdFactura,
                            f.Fecha,
                            f.Cliente,
                            f.Total
                        })
                        .ToList(); // Convertir a lista para mostrar en DataGridView

        // Mostrar en DataGridView
        dgvFacturas.DataSource = factura;

        // Mostrar mensaje si no hay resultados
        if (factura.Count == 0)
        {
            MessageBox.Show("Factura no encontrada.", "Información", MessageBoxButtons.OK, MessageBoxIcon.Information);
        }
    }
}
