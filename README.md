import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { useState } from "react";
import { ShoppingCart, Download } from "lucide-react";

const products = [
  {
    id: 1,
    name: "eBook Desain Feed Instagram",
    image: "/products/ebook-feed.jpg",
    price: "Rp 25.000",
    description: "Panduan lengkap membuat feed Instagram yang menarik dan estetik.",
    paymentInfo: "Bayar ke DANA 0812-XXXX-XXXX dan kirim bukti ke WhatsApp."
  },
  {
    id: 2,
    name: "Poster Digital - Motivasi",
    image: "/products/poster-motivasi.jpg",
    price: "Rp 15.000",
    description: "Poster digital siap cetak dengan kutipan motivasi terbaik.",
    paymentInfo: "Bayar ke DANA 0812-XXXX-XXXX dan kirim bukti ke WhatsApp."
  }
];

export default function HomePage() {
  const [selected, setSelected] = useState(null);

  return (
    <div className="max-w-5xl mx-auto px-4 py-10">
      <h1 className="text-4xl font-bold mb-6 text-center">cloth.id - Toko Produk Digital</h1>
      <p className="text-center mb-10 text-muted-foreground">
        Jual eBook desain & poster digital siap pakai.
      </p>

      <div className="grid md:grid-cols-2 gap-6">
        {products.map((product) => (
          <Card key={product.id} className="hover:shadow-xl transition-shadow">
            <img
              src={product.image}
              alt={`Gambar ${product.name}`}
              className="w-full h-60 object-cover rounded-t-2xl"
            />
            <CardContent className="p-4">
              <h2 className="text-xl font-semibold">{product.name}</h2>
              <p className="text-sm text-muted-foreground mb-2">{product.description}</p>
              <div className="flex items-center justify-between mt-4">
                <span className="font-bold text-lg">{product.price}</span>
                <Button onClick={() => setSelected(product)}>
                  <ShoppingCart className="w-4 h-4 mr-2" /> Beli
                </Button>
              </div>
            </CardContent>
          </Card>
        ))}
      </div>

      {selected && (
        <div
          className="fixed inset-0 bg-black/60 flex items-center justify-center z-50"
          onClick={() => setSelected(null)}
        >
          <div
            className="bg-white rounded-2xl p-6 max-w-md w-full shadow-xl"
            onClick={(e) => e.stopPropagation()}
          >
            <h2 className="text-2xl font-bold mb-2">{selected.name}</h2>
            <p className="mb-4">{selected.description}</p>
            <p className="mb-4">Harga: <strong>{selected.price}</strong></p>
            <p className="mb-4">{selected.paymentInfo}</p>
            <p className="text-sm text-muted-foreground mb-6">
              Setelah pembayaran, kirim bukti ke WhatsApp untuk menerima file PDF.
            </p>
            <div className="flex justify-end gap-2">
              <Button variant="ghost" onClick={() => setSelected(null)}>Tutup</Button>
              <Button>
                <Download className="w-4 h-4 mr-2" /> Bayar Sekarang
              </Button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}
